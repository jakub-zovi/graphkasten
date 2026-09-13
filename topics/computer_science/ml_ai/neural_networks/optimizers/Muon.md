---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/optimizers
created: 2026-02-15T10:31
modified: 2026-07-26T13:31
published:
sources:
  - "[From AdamW to Muon Optimizer](https://athekunal.medium.com/from-adamw-to-muon-optimizer-cf67d43fb9e9)"
topics:
  - Optimizers
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Muon
- Muon is a new optimizer that was used in [[Kimi2]] training and achieved SOTA performance
# Resources
- [Muon is scalable for LLM training](https://arxiv.org/pdf/2502.16982)
	- 2025-02-24
	- 47 citations
- [Muon Outperforms Adam in Tail-End Associative Memory Learning](https://arxiv.org/pdf/2509.26030)
	- 2025-09-30
	- 2 citations
- [From AdamW to Muon Optimizer](https://athekunal.medium.com/from-adamw-to-muon-optimizer-cf67d43fb9e9)
	- 2025-07-22
	- This note aggregate content mainly from this article
# [From AdamW to Muon Optimizer](https://athekunal.medium.com/from-adamw-to-muon-optimizer-cf67d43fb9e9)
## WHY DO WE NEED A NEW OPTIMIZER?
- Adam and AdamW require two things: (i) the first moment, (ii) the second moment. These are generally stored in full precision (fp32 or tf32), which consumes 8 (4 for the first moment and 4 for the second moment) times the number of weight parameters.
- Also, as these are moving averages, we need to do an all-gather for the gradients to compute the first and second moments, which incurs a lot of communication overhead
- Need for orthogonality (below is a snippet from the muon optimizer [blog post](https://kellerjordan.github.io/posts/muon/))
> And for an empirically-flavored motivation, we observe that based on manual inspection, the updates produced by both SGD-momentum and Adam for the 2D parameters in transformer-based neural networks typically have very high condition number. That is, they are almost low-rank matrices, with the updates for all neurons being dominated by just a few directions. We speculate that orthogonalization effectively increases the scale of other “rare directions” which have small magnitude in the update but are nevertheless important for learning.
- We apply normalization in various forms, such as layer normalization within layers, batch normalization across batches, and normalized weight initialization. These practices suggest that normalization helps improve generalization and contributes to faster convergence during training. **Why not normalize the gradients too?**
## MUON

- The formulation of muon is really simple; instead of keeping track of the first and second moment, it only has the momentum (Nesterov momentum). It normalizes the momentum matrix before doing the weight update
- For normalization, it uses Newton-Schulz instead of Singular Value Decomposition (SVD). SVD has a time complexity of O(mn²) for a matrix of size R^{m x n}. We will be applying normalization to big feed-forward layers, which will incur a lot of computational overhead. Hence, the authors use the Newton-Schulz method
- The PyTorch code

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1400/1*n5f1KxR2Ddla8d-gyXEnvg.png)

Newton Schulz degree 5 polynomial

```python
# Pytorch code
def newtonschulz5(G, steps=5, eps=1e-7):
    assert G.ndim == 2
    #the coefficients derived empirically 
    a, b, c = (3.4445, -4.7750, 2.0315)
    X = G.bfloat16()
    #normalize the matrix with the max-norm so that values
    #have a range of (0,1)
    X /= (X.norm() + eps)
    #We are going matmul the X matrix with its transpose
    #which will be of dimension row x row. 
    #To reduce computational complexity, the row < column 
    #hence take a transpose
    if G.size(0) > G.size(1):
        X = X.T
    for _ in range(steps):
        A = X @ X.T
        #b and c are scalar-matrix multiplication
        #c is multiplied with degree 5 (X @ X.T squares the matrix)
        B = b * A + c * A @ A
        X = a * X + B @ X
    #flip back the dimension
    if G.size(0) > G.size(1):
        X = X.T
    return X
```

- **One neat trick was the flipping of the matrix so that we always work with a fat matrix (larger columns than rows) rather than a tall matrix (smaller columns). This reduces the number of dimensions in the matrix X @ X.T**
- In the blog post, the authors used Nesterov momentum instead of SGD momentum. **In the former, we first go in the direction of momentum and then go in the direction of gradients. This produces more stable updates as compared to having unstable updates from the gradients of a batch.**
- Another improvement as compared to Adam is having only one buffer instead of 2. Adam had a first and second moment buffer, but Muon only has one buffer for momentum. **That reduces the memory footprint by 50% (from 8 bytes to 4 bytes) per parameter.**

![](https://miro.medium.com/v2/resize:fit:808/1*iKorIl1YDZCszgQvshoUmQ.png)

Muon optimizer in Muon Clip [paper](https://arxiv.org/html/2502.16982v1) from the Kimi team

The Mt is Nesterov momentum

- Muon is steepest descent under norm constraints: In muon, we have gradient updates where the updates are normalized and lie in the Schatten p-norm (or the norm of the singular values in SVD). If we take the max of the singular values in SVD, we get the spectral norm, which is used in PCA. Also, the normalization is static, hence we get stable updates
- Adam and AdamW have a dynamic adaptation to the momentum; hence, all the weight dimensions get updated dynamically, which might lack stability in updates

## SCALING UP MUON

In the Muon clip paper, the authors did a few more tricks to scale the muon

### WEIGHT DECAY

- They added the weight decay to the update as they observed the weights and RMS norm kept increasing with more training

![](https://miro.medium.com/v2/resize:fit:1056/1*uMXNRwBbYxejcAkD_Gs33A.png)

### SCALING (MULTIPLYING) BY THE DIMENSION OF THE MATRIX

- Let’s say the dimension of the matrix is A x B. **In the Newton-Schulz schulz, we normalize the matrix by the dimensions, hence for larger matrices, the updates would be smaller, and for smaller matrices (head dimension of the Q, K and V projection matrices) would be larger.** Hence, the authors scale up the updates by the square root of the matrix dimensions

### MATCHING THE RMS NORM UPDATE OF ADAM

- In this blog [post](https://jeremybernste.in/writing/deriving-muon), Muon is used for linear matrices only, not for non-matrix operations like the embedding dimension,n which has one-hot input. This sparsity would mess up the normalization.
- Hence, AdamW is still used for these matrices like RMSNorm, LM head and embedding parameters. As we keep the hyperparameters the same for Muon and AdamW, we need to match the RMS norm of AdamW
- Empirically, it is around 0.2 to 0.4; hence, the authors scale the updates by 0.2. Finally, we have

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1400/1*_CrTh2ofyozrYr82m6lsaQ.png)

Scalable muon update equation

Note: The authors used 5 iterations of Newton-Schulz, where we do the normalization iteratively 5 times on the gradient matrix.

## TAKEAWAYS FROM THE PAPER

- Muon optimizes along more number of dimensions as compared to AdamW. This is evident from the SVD entropy over timesteps plot from the paper

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1400/1*xamk2lpf5kOP6jyEq_lqBg.png)

SVD entropy of Muon is higher, more updates along varied number of dimensions

- Muon for SFT works well if the pre-training optimizer was Muon too.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1400/1*pNUVsU0mu7mnY4Dq9SQQew.png)

This brings to the end of our blog post. If you have any queries, then I am one comment away