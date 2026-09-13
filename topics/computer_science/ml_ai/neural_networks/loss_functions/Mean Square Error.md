---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-09-30T14:35
modified: 2026-02-15T10:59
published:
sources:
  - ChatGPT
topics:
  - Loss Functions
authors:
ai-assisted:
hidden:
public: true
---
# Mean Squared Error (MSE)
Used for **[[regression]]** tasks, where the target variable is **continuous** (e.g. house price, temperature, stock value).

$$  
MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2  
$$

- $n$ = number of samples
- $y_i$ = true (ground-truth) value
- $\hat{y}_i$ = predicted value

Interpretation:
- Measures the **average squared difference** between predicted and true values.
- Squaring penalizes **large errors more strongly** than small ones.
- The loss is always **non-negative** and equals 0 only when predictions are perfect.

Properties:
- Differentiable and smooth → works well with gradient-based optimization.
- Sensitive to **outliers** due to the squared term.
- Assumes errors are normally distributed (underlying statistical interpretation).