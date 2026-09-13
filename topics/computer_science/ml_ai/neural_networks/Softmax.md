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
# Softmax
- Generalizes [[Sigmoid]] to multi-class settings. Converts a vector of raw scores ([[Logit|logits]]) into a **probability distribution** that sums to 1.
$$
\text{softmax}(x_i) = \frac{e^{x_i}}{\sum_{j} e^{x_j}}
$$

- Output probabilities sum to 1 across all classes
- Used in **multi-class classification** output layers
- Numerically stabilized in practice by subtracting $\max(x)$ from all [[Logit|logits]] before exponentiation
