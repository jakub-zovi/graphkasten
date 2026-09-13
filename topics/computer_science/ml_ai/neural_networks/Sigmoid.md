---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2026-03-21T00:00
modified: 2026-07-26T13:35
published:
sources:
topics:
  - Activation Functions
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Sigmoid
S-shaped activation that squashes any real value into the range $(0, 1)$.
$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

- Output is a smooth probability-like score
- Used in **binary classification** output layers
- Gradient vanishes for very large or very small inputs (**vanishing gradient** problem)
- Computationally more expensive than ReLU due to the exponential
