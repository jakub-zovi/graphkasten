---
tags:
  - ml_ai
  - ml_ai/neural_nets
created:
modified: 2025-08-09T11:32
published:
sources:
topics:
  - Residual Blocks
  - Skip Connections
  - Backpropagation
  - Vanishing Gradients
authors:
ai-assisted:
hidden:
public: true
---
# Residual Block
![[residual_block.png]]
### 1. Gradient Through the Addition (Skip Connection):
In the residual block, after computing the output of the transformation $\mathcal{F}(x)$ (through weight layers and activation functions), the output is added element-wise to the input $x$ via the skip connection. This addition is crucial and impacts backpropagation.

Given that $y = g(x + \mathcal{F}(x))$, where $g(\cdot)$ is the activation function applied after the addition:

- The gradient of the loss w.r.t. $y$ is passed through $g(\cdot)$, and then this gradient splits at the addition point into two paths:
  $$
  \frac{\partial L}{\partial (x + \mathcal{F}(x))} = \frac{\partial L}{\partial y} \odot g'(x + \mathcal{F}(x))
  $$
  Here, $g'(\cdot)$ is the derivative of the activation function $g(\cdot)$.

- Since $y = x + \mathcal{F}(x)$, we distribute the gradient evenly between $x$ and $\mathcal{F}(x)$ due to the element-wise nature of the addition operation:
  $$
  \frac{\partial L}{\partial x} = \frac{\partial L}{\partial (x + \mathcal{F}(x))}
  $$
  $$
  \frac{\partial L}{\partial \mathcal{F}(x)} = \frac{\partial L}{\partial (x + \mathcal{F}(x))}
  $$

### 2. Combining the Gradients for $x$:
Once we've backpropagated through the transformation $\mathcal{F}(x)$ (the weight layers, activation functions, etc.), we get another gradient w.r.t. $x$, which we denote as $\frac{\partial L}{\partial x_{\mathcal{F}}}$. This gradient represents the contribution of the path through the transformation.

Since the skip connection directly connects $x$ to the output, the total gradient w.r.t. $x$ is the **sum** of the gradients from the two paths:
- The gradient coming from the identity path: $\frac{\partial L}{\partial x}$.
- The gradient coming from the transformed path $\mathcal{F}(x)$: $\frac{\partial L}{\partial x_{\mathcal{F}}}$.

Thus, the total gradient w.r.t. $x$ is:
$$
\frac{\partial L}{\partial x_{\text{total}}} = \frac{\partial L}{\partial (x + \mathcal{F}(x))} + \frac{\partial L}{\partial x_{\mathcal{F}}}
$$

### Summary of Additional Steps in a Residual Block:
1. **Gradient through the addition**: The gradient splits at the addition point, with one path going through the skip connection and the other through the transformation $\mathcal{F}(x)$.
2. **Combining gradients**: After backpropagating through $\mathcal{F}(x)$, sum the two gradients from the skip path and the transformation path to compute the total gradient with respect to $x$.

These are the additional steps unique to residual blocks that differentiate them from standard backpropagation in a fully connected network. The skip connection allows gradients to flow more easily and helps prevent issues like vanishing gradients, particularly in deep networks.

## Extension
- [[Attention Residuals]] — replaces the fixed uniform skip connection with learned, input-dependent softmax attention over all prior layer outputs