---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/regularization
created: 2026-03-15T09:28
modified: 2026-07-26T13:37
published:
sources:
  - "[Deep Learning (Goodfellow et al., 2016) — Chapter 7](https://www.deeplearningbook.org/contents/regularization.html)"
  - "[An Introduction to Statistical Learning (James et al., 2021) — Chapter 6](https://www.statlearning.com/)"
topics:
  - Regularization
  - Sparsity
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# L1 Regularization
L1 regularization (also called **Lasso** in the statistics literature) **adds the sum of absolute values of the weights to the training loss** ([[absolute sum of weights + loss]]). It encourages the model to **[[drive unimportant weights exactly to zero]]**, producing sparse solutions ([Deep Learning, Ch. 7](https://www.deeplearningbook.org/contents/regularization.html)).

## Penalized Loss
$$
\mathcal{L}_{\text{L1}} = \mathcal{L} + \lambda \sum_{i} |w_i|
$$

where:
- $\mathcal{L}$ is the original loss (e.g. cross-entropy)
- $\lambda > 0$ is the regularization strength
- $w_i$ are the model weights

## Gradient Update
$$
\frac{\partial \mathcal{L}_{\text{L1}}}{\partial w_i} = \frac{\partial \mathcal{L}}{\partial w_i} + \lambda \cdot \text{sign}(w_i)
$$

The subgradient $\text{sign}(w_i)$ applies a constant push toward zero, regardless of magnitude — so small weights are driven all the way to 0.

## Properties
- Produces **sparse** weight vectors (many exactly-zero weights) — useful for feature selection
- Non-differentiable at $w_i = 0$; handled via subgradients or proximal operators
- Less common in deep learning than L2; more common in linear models and sparse coding
- Equivalent to placing a **Laplace prior** on weights from a Bayesian perspective

## Comparison with [[L2 Regularization]]
| | L1 | L2 |
|---|---|---|
| Penalty | $\sum |w_i|$ | $\sum w_i^2$ |
| Effect | Sparse (zeros out weights) | Dense (shrinks all weights) |
| Geometry | Diamond constraint | Sphere constraint |
| Differentiability | No (at 0) | Yes |
