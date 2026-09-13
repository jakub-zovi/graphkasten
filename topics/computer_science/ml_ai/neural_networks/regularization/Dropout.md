---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/regularization
created: 2026-03-15T09:28
modified: 2026-07-26T13:37
published:
sources:
  - "[Dropout: A Simple Way to Prevent Neural Networks from Overfitting (Srivastava et al., 2014)](https://jmlr.org/papers/v15/srivastava14a.html)"
  - "[Deep Learning (Goodfellow et al., 2016) — Chapter 7](https://www.deeplearningbook.org/contents/regularization.html)"
topics:
  - Regularization
  - Stochastic Training
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Dropout
Dropout is a regularization technique that randomly sets a fraction of neuron activations to zero during each forward pass of training. This prevents neurons from co-adapting and forces the network to learn redundant representations ([Srivastava et al., 2014](https://jmlr.org/papers/v15/srivastava14a.html)).

## Mechanism
During training, each activation $h_i$ is independently zeroed with probability $p$ (the **drop rate**):
$$
\tilde{h}_i = h_i \cdot \text{Bernoulli}(1 - p)
$$

At inference, all neurons are active but outputs are scaled by $(1 - p)$ to match expected training values (or equivalently, training uses **inverted dropout** — scale by $\frac{1}{1-p}$ at train time so no change is needed at test time).

## Ensemble Interpretation
Training with dropout approximates training an ensemble of $2^n$ thinned networks (where $n$ is the number of units). At test time, the full network with scaled weights approximates geometric mean of the ensemble ([Deep Learning, Ch. 7](https://www.deeplearningbook.org/contents/regularization.html)).

## Properties
- Computationally cheap: random masking adds minimal overhead
- Works well for fully-connected and recurrent layers; less effective for convolutional layers (use [[Batch Normalization]] instead)
- Typical drop rates: $p = 0.5$ for hidden layers; $p = 0.1$–$0.2$ for input/embedding layers
- Transformers use attention dropout and residual dropout in addition to MLP dropout
- Creates a form of **noise injection** during training, improving robustness

## Variants
- **DropConnect** — drops individual weights rather than activations
- **Spatial Dropout** — drops entire feature maps (used in CNNs)
- **Monte Carlo Dropout** — keep dropout active at test time to estimate prediction uncertainty
