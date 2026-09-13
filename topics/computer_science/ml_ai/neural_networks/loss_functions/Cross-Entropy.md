---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-09-30T14:36
modified: 2026-07-26T13:36
published:
sources:
  - ChatGPT
topics:
  - Loss Functions
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Cross-Entropy
- Cross-entropy **measures how different two probability distributions are** 
	- Unlike [[Entropy]] which measures the uncertainty inside a single probability distribution
- Use for multi-class classification tasks i.e. labels are dependent. Because in **[[multi-class classification]]**, each sample belongs to exactly **one** class from a set of mutually exclusive classes (e.g. image with cat can not contain a dog). 
$$
 CCE = - \sum_{i=1}^{n} y_i \log(\hat{y}_i)
 $$
* $y_i$ = the true label for class $i$.
	* Typically encoded as a **one-hot vector** (so $y_i = 1$ for the correct class, and $0$ otherwise).
* $\hat{y}_i$ = the **predicted probability** that the model assigns to class $i$.
	* These are the outputs of a **softmax** layer, i.e. $\hat{y}_i \in [0,1]$ and $\sum_i \hat{y}_i = 1$.
- So in words:
	* $y_i$ is the ground-truth distribution.
	* $\hat{y}_i$ is the model’s predicted distribution.
- The loss penalizes the model if it assigns low probability to the true class.
## Sources
- [But what is cross-entropy? | Compression is Intelligence Part 2](https://www.youtube.com/watch?v=GlYgs6v2YfU&t=573s)
## Intuition
### Why Cross-Entropy and Not MSE?
- [[MSE]] treats all errors as equally costly in a quadratic sense — it's designed for continuous outputs where the distance between prediction and target is meaningful
- In classification, we output **probabilities**, not continuous values, so the geometry is fundamentally different
- **Vanishing gradients with MSE + softmax:**
	- When the predicted probability is far from the true label (model is very wrong), the sigmoid/softmax saturates and MSE produces near-zero gradients → training stalls
	- Cross-entropy avoids this: its gradient with respect to the logit simplifies to just $\hat{y}_i - y_i$, which is large when the model is confidently wrong
- **Cross-entropy directly measures probabilistic mismatch**, making it the natural fit for the softmax output layer

### Why Logarithm?
- Directly maximizing predicted probability $\hat{y}_c$ (where $c$ is the correct class) would work in theory, but log turns that into a sum, which is numerically stable and mathematically convenient
- $\log$ heavily penalizes confidently wrong predictions: if the model assigns $\hat{y}_c = 0.01$ to the correct class, $-\log(0.01) = 4.6$; if it assigns $0.99$, $-\log(0.99) \approx 0.01$
- The sharp penalty forces the model to be **calibrated** — not just right, but confidently right

### Information-Theoretic View
- From information theory: cross-entropy $H(p, q) = -\sum_i p_i \log q_i$ is the expected number of bits needed to encode events from distribution $p$ using a code optimized for $q$
- Minimizing cross-entropy = minimizing the "extra cost" of using the model's predicted distribution $\hat{y}$ instead of the true distribution $y$
- This equals [[KL Divergence]] $D_{KL}(y \| \hat{y})$ up to a constant (the entropy of the true labels), so minimizing cross-entropy also minimizes the KL divergence between the true and predicted distributions

### Connection to Maximum Likelihood Estimation
- Cross-entropy loss is equivalent to **negative log-likelihood** under a categorical distribution
- Minimizing the average cross-entropy over all training examples = maximizing the likelihood that the model would have generated the observed labels
$$
\mathcal{L} = -\frac{1}{N}\sum_{n=1}^{N} \log \hat{y}_{c_n}
$$
where $c_n$ is the correct class index for sample $n$ — this is just the log-probability the model assigned to the right answer, averaged across the dataset
