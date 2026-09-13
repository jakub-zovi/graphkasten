---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-09-30T14:33
modified: 2026-09-06T10:24
published:
sources:
topics:
  - Loss Functions
authors:
  - ChatGPT
ai-assisted:
hidden:
public: true
---
# Binary Cross-Entropy
Used for **[[multi-label classification]]**, each sample can belong to **multiple classes** simultaneously. The classes are **not mutually exclusive**, and each class is treated as a separate binary classification task. Therefore, each label is independent and can be treated as a separate binary classification.

$$

BCE = - \sum_{i=1}^{C} \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]
$$
* $y_i \in \{0,1\}$: the true label for class $i$.
* $\hat{y}_i \in (0,1)$: the predicted probability for class $i$ (from a sigmoid).

Interpretation:

* If $y_i = 1$, the loss is $-\log(\hat{y}_i)$ → penalizes low predicted probability for the positive class.
* If $y_i = 0$, the loss is $-\log(1-\hat{y}_i)$ → penalizes high predicted probability for the negative class.