---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/regularization
created: 2026-03-15T09:28
modified: 2026-07-26T13:38
published:
sources:
  - "[Deep Learning (Goodfellow et al., 2016) — Chapter 7](https://www.deeplearningbook.org/contents/regularization.html)"
  - "[An Introduction to Statistical Learning (James et al., 2021) — Chapter 6](https://www.statlearning.com/)"
topics:
  - Regularization
  - Weight Penalization
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# L2 Regularization
L2 regularization (also called **Ridge** in statistics, or **weight decay** in the SGD context) penalizes the sum of squared weights. It [[keeps all weights small but non-zero]], smoothly shrinking them toward zero ([Deep Learning, Ch. 7](https://www.deeplearningbook.org/contents/regularization.html)).

## Penalized Loss
$$
\mathcal{L}_{\text{L2}} = \mathcal{L} + \frac{\lambda}{2} \sum_{i} w_i^2
$$

where:
- $\mathcal{L}$ is the original loss
- $\lambda > 0$ is the regularization strength
- $\frac{1}{2}$ is a convenience factor that cancels the coefficient in the gradient

## Gradient Update
$$
\frac{\partial \mathcal{L}_{\text{L2}}}{\partial w_i} = \frac{\partial \mathcal{L}}{\partial w_i} + \lambda w_i
$$

The update rule becomes:
$$
w_i \leftarrow w_i - \alpha \left(\frac{\partial \mathcal{L}}{\partial w_i} + \lambda w_i\right) = (1 - \alpha \lambda)\, w_i - \alpha \frac{\partial \mathcal{L}}{\partial w_i}
$$

The factor $(1 - \alpha \lambda)$ shrinks the weight at each step — this is exactly [Weight Decay](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Fregularization%2FWeight%20Decay) in SGD.

## Properties
- Smooth and differentiable everywhere — easy to optimize
- Produces **dense** solutions: all weights shrink but rarely reach zero
- Equivalent to placing a **Gaussian prior** on weights (MAP estimation)
- In SGD: identical to [Weight Decay](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Fregularization%2FWeight%20Decay)
- In Adam: **not** identical to weight decay — the gradient scaling distorts the L2 penalty; see [Adamw](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FAdamw) for the decoupled fix

## Bayesian Interpretation
Minimizing $\mathcal{L}_{\text{L2}}$ is equivalent to MAP estimation with a Gaussian prior $p(w) \propto e^{-\frac{\lambda}{2}\|w\|^2}$.

## Comparison with [[L1 Regularization]]
| | L1 | L2 |
|---|---|---|
| Penalty | $\sum |w_i|$ | $\sum w_i^2$ |
| Effect | Sparse (zeros out weights) | Dense (shrinks all weights) |
| Geometry | Diamond constraint | Sphere constraint |
| Differentiability | No (at 0) | Yes |
