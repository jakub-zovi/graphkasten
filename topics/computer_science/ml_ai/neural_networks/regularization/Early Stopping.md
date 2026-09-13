---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/regularization
created: 2026-03-15T09:28
modified: 2026-07-26T13:37
published:
sources:
  - "[Deep Learning (Goodfellow et al., 2016) — Chapter 7](https://www.deeplearningbook.org/contents/regularization.html)"
  - "[Pattern Recognition and Machine Learning (Bishop, 2006) — Chapter 5](https://www.microsoft.com/en-us/research/uploads/prod/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf)"
topics:
  - Regularization
  - Training Strategy
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Early Stopping
Early stopping halts training when the validation loss stops improving, using the model checkpoint from the best validation epoch. It is the cheapest regularization method — no extra computation, no hyperparameter penalty terms, no architectural changes ([Deep Learning, Ch. 7](https://www.deeplearningbook.org/contents/regularization.html)).

## Mechanism
1. Monitor validation loss after every epoch (or every $k$ steps)
2. Save a checkpoint whenever validation loss reaches a new minimum
3. Stop training if validation loss has not improved for $P$ consecutive checks (**patience**)
4. Restore the saved checkpoint as the final model

## Regularization Effect
Early stopping limits the effective number of training iterations, which bounds the complexity of the learned function. Goodfellow et al. show that for quadratic loss, early stopping is approximately equivalent to [L2 Regularization](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Fregularization%2FL2%20Regularization) with $\lambda \approx \frac{1}{\tau \epsilon}$, where $\tau$ is the number of steps and $\epsilon$ is the learning rate ([Deep Learning, Ch. 7](https://www.deeplearningbook.org/contents/regularization.html)).

## Key Hyperparameters
| Parameter | Typical Value | Description |
|---|---|---|
| Patience $P$ | 5–20 epochs | Steps without improvement before stopping |
| Min delta | $10^{-4}$–$10^{-3}$ | Minimum change to count as improvement |
| Restore best weights | Yes | Revert to best checkpoint after stopping |

## Properties
- No additional compute cost during forward/backward pass
- Works with any optimizer and architecture
- Implicitly limits model complexity by capping effective training time
- Can be combined with learning rate schedules — stop only after LR has been reduced
- Risk: stopping too early if validation is noisy; mitigated by larger patience or smoothing
