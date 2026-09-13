---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/regularization
created: 2026-03-15T09:28
modified: 2026-07-26T13:38
published:
sources:
  - "[Deep Learning (Goodfellow et al., 2016) — Chapter 7](https://www.deeplearningbook.org/contents/regularization.html)"
topics:
  - Regularization
  - Overfitting
  - Generalization
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Regularization
Regularization refers to any technique that reduces generalization error (overfitting) without necessarily reducing training error. Most methods add a penalty, constraint, or structural change that discourages the model from fitting noise in the training set ([Deep Learning, Ch. 7](https://www.deeplearningbook.org/contents/regularization.html)).

## Methods
- [[L1 Regularization]]
	- Adds sum of absolute weights to the loss; promotes sparse weight vectors
- [[L2 Regularization]]
	- Adds sum of squared weights to the loss; shrinks all weights smoothly toward zero
- [[Weight Decay]]
	- Directly decays weights each step; equivalent to L2 in SGD, decoupled in Adam ([[Adamw]])
- [[Dropout]]
	- Randomly zeroes activations during training; acts as ensemble of thinned networks
- [[Early Stopping]]
	- Halts training when validation loss stops improving; cheapest form of regularization
- [[Batch Normalization]]
	- Normalizes layer inputs per mini-batch; has an implicit regularizing effect
