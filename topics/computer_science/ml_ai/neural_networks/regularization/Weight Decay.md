---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/regularization
created: 2026-03-15T09:28
modified: 2026-07-26T13:38
published:
sources:
  - "[Decoupled Weight Decay Regularization (Loshchilov & Hutter, 2019)](https://arxiv.org/abs/1711.05101)"
  - "[Deep Learning (Goodfellow et al., 2016) — Chapter 7](https://www.deeplearningbook.org/contents/regularization.html)"
topics:
  - Regularization
  - Weight Penalization
  - Optimizers
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Weight Decay
Weight decay is a regularization technique that directly reduces each weight by a small fraction at every update step, independent of the gradient. It was originally proposed as a simple mechanism to prevent weights from growing unboundedly.

## Update Rule
$$
w_t \leftarrow (1 - \eta \lambda)\, w_t - \eta \nabla_w \mathcal{L}
$$

where:
- $\eta$ is the learning rate
- $\lambda$ is the weight decay coefficient
- The factor $(1 - \eta \lambda)$ decays the weight directly

## Relationship with L2 Regularization
In **SGD**, weight decay and [L2 Regularization](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Fregularization%2FWeight%20Decay) are mathematically equivalent:
$$
w \leftarrow w - \eta(\nabla \mathcal{L} + \lambda w) = (1 - \eta\lambda) w - \eta \nabla \mathcal{L}
$$

In **Adam**, they diverge. Adam scales gradients by an adaptive factor $\frac{1}{\sqrt{\hat{v}_t} + \epsilon}$, which also scales the L2 gradient penalty — distorting it away from a true weight decay. **Decoupled weight decay** (used in [Adamw](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Fregularization%2FWeight%20Decay)) applies the decay directly to weights, bypassing the gradient scaling ([Loshchilov & Hutter, 2019](https://arxiv.org/abs/1711.05101)).

## Coupled vs Decoupled
| | L2 in Adam | Weight Decay (AdamW) |
|---|---|---|
| Penalty applied to | Gradient (then scaled) | Weights directly |
| Effect | Distorted by adaptive LR | Clean, uniform shrinkage |
| Recommended | No | Yes |

## Properties
- Computationally free: just a scalar multiply on weights per step
- Decoupled weight decay (AdamW) is the current standard for transformer training
- Typical values: $\lambda \in [10^{-4}, 10^{-1}]$
