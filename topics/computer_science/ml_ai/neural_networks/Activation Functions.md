---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-10-08T09:23
modified: 2026-03-22T10:09
published:
sources:
  - ChatGPT
topics:
  - Activation Functions
authors:
ai-assisted:
hidden:
public: true
---
# Activation Functions
This note aggregates information about different activation functions.
## [[Unit Step]]
Binary threshold activation. Outputs 1 if input is non-negative, otherwise 0.
$$
f(x) =
\begin{cases}
1 & \text{if } x \ge 0 \
0 & \text{if } x < 0
\end{cases}
$$

* Non-differentiable at ( x = 0 )
* Used in early perceptron models
---
## [[ReLU]]
Rectified Linear Unit. Outputs input if positive, otherwise 0.
$$
f(x) = \max(0, x)
$$

* Computationally efficient
* Helps mitigate vanishing gradients
* Can suffer from "dying ReLU" problem
---
## [[Leaky ReLU]]
Variant of ReLU allowing small negative slope for negative inputs.
$$
f(x) =
\begin{cases}
x & \text{if } x > 0 \
\alpha x & \text{if } x \le 0
\end{cases}
$$

* ( \alpha ) is small (e.g., 0.01)
* Reduces dying ReLU issue
---
## [[SELU]]
Scaled Exponential Linear Unit. Self-normalizing activation.
$$
f(x) =
\begin{cases}
\lambda x & \text{if } x > 0 \
\lambda \alpha (e^x - 1) & \text{if } x \le 0
\end{cases}
$$

* Typical constants: ( \alpha \approx 1.6733 ), ( \lambda \approx 1.0507 )
* Promotes self-normalizing neural networks
* Designed for deep feedforward networks
---
## [[Sigmoid]]
S-shaped function squashing inputs to $(0, 1)$.
$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

* Used in binary classification output layers
* Suffers from vanishing gradients at extremes
---
## [[Softmax]]
Generalizes Sigmoid to multi-class output. Converts logits to a probability distribution summing to 1.
$$
\text{softmax}(x_i) = \frac{e^{x_i}}{\sum_{j} e^{x_j}}
$$

* Used in multi-class classification output layers