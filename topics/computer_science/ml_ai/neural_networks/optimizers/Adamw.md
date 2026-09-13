---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/optimizers
created: 2026-03-09T10:00
modified: 2026-09-06T10:24
published:
sources:
  - "[Decoupled Weight Decay Regularization](https://arxiv.org/abs/1711.05101)"
topics:
  - Optimizers
  - Weight Decay
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# AdamW
- AdamW is a variant of [[Adam]] that decouples weight decay from the gradient-based update. Introduced by Loshchilov & Hutter (2019).

## Motivation: L2 Reg ≠ Weight Decay in Adam
- In SGD, adding L2 regularization ($\frac{\lambda}{2}\|\theta\|^2$ to the loss) is mathematically equivalent to applying weight decay directly to the weights
- In Adam this equivalence **breaks**: the adaptive scaling by $\hat{v}_t$ modifies the effective magnitude of L2 regularization per parameter, so parameters with large gradients receive less regularization than parameters with small gradients
- This means Adam + L2 does not regularize uniformly, leading to suboptimal generalization

## Decoupled Weight Decay
AdamW separates the weight decay step from the gradient update:

$$
\theta_t = \theta_{t-1} - \alpha \left( \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon} + \lambda\, \theta_{t-1} \right)
$$

where:
- $\theta_t$ is the parameter vector being updated
- $\alpha$ is the learning rate
- $\hat{m}_t$ is the bias-corrected first moment (mean of gradients) from [[Adam]]
- $\hat{v}_t$ is the bias-corrected second moment (mean of squared gradients) from [[Adam]]
- $\epsilon$ is a small constant for numerical stability (avoids division by zero)
- $\lambda$ is the weight decay coefficient applied directly to the weights, independent of the adaptive gradient scaling

## Difference from Adam
| Aspect | Adam | AdamW |
|---|---|---|
| Regularization | L2 added to loss (gradient) | Weight decay applied directly to weights |
| Effective decay | Scaled by $1/\sqrt{\hat{v}_t}$ per param | Uniform $\lambda$ per param |
| Generalization | Weaker | Stronger |

## Usage
- AdamW is the default optimizer for most modern LLM training (GPT, BERT, LLaMA)
- It is also used as the baseline optimizer in hybrid setups like [[Muon]], which applies AdamW to embedding and normalization parameters
