---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/regularization
created: 2026-03-15T09:28
modified: 2026-07-26T13:37
published:
sources:
  - "[Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift (Ioffe & Szegedy, 2015)](https://arxiv.org/abs/1502.03167)"
  - "[How Does Batch Normalization Help Optimization? (Santurkar et al., 2018)](https://arxiv.org/abs/1805.11604)"
topics:
  - Regularization
  - Normalization
  - Training Stability
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Batch Normalization
Batch Normalization (BatchNorm) normalizes layer inputs across the mini-batch dimension, then applies learned affine parameters. Originally motivated by reducing internal covariate shift, it has since been shown to primarily improve optimization landscape smoothness and has an implicit regularizing effect ([Ioffe & Szegedy, 2015](https://arxiv.org/abs/1502.03167)).

## Mechanism
For a mini-batch $\mathcal{B} = \{x_1, \ldots, x_m\}$:
$$
\mu_\mathcal{B} = \frac{1}{m} \sum_{i=1}^m x_i, \quad \sigma^2_\mathcal{B} = \frac{1}{m} \sum_{i=1}^m (x_i - \mu_\mathcal{B})^2
$$
$$
\hat{x}_i = \frac{x_i - \mu_\mathcal{B}}{\sqrt{\sigma^2_\mathcal{B} + \epsilon}}
$$
$$
y_i = \gamma \hat{x}_i + \beta
$$

where $\gamma$ and $\beta$ are **learned** scale and shift parameters.

## Regularizing Effect
- Adds stochastic noise (batch statistics vary between batches), which acts similarly to [[Dropout]]
- Often reduces the need for dropout when used in CNNs
- Larger batch sizes reduce the noise effect and weaken regularization

## Optimization Benefits
- Smooths the loss landscape, enabling higher learning rates ([Santurkar et al., 2018](https://arxiv.org/abs/1805.11604))
- Reduces sensitivity to weight initialization

## Variants
- **Layer Normalization (LayerNorm)** — normalizes across features instead of batch; standard in transformers
- **Instance Normalization** — normalizes per sample per channel; used in style transfer
- **Group Normalization** — normalizes within groups of channels; useful for small batch sizes
- **RMSNorm** — simplified LayerNorm without mean centering; used in LLaMA and modern LLMs
