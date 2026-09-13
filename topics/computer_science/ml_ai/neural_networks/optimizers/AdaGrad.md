---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/optimizers
created: 2026-03-09T10:00
modified: 2026-07-26T13:32
published:
sources:
  - "[Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](https://jmlr.org/papers/v12/duchi11a.html)"
topics:
  - Optimizers
  - Adaptive Learning Rate
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# AdaGrad
AdaGrad (Adaptive Gradient Algorithm) [[adapts the learning rate per parameter]] based on the history of squared gradients. Introduced by Duchi et al. (2011).
## Key Idea
- Parameters that receive large or frequent gradient updates get a smaller effective learning rate
- Parameters that receive small or infrequent updates get a larger effective learning rate
- Particularly useful for sparse features (e.g., NLP, recommender systems)

## Update Rule
$$
G_t = G_{t-1} + g_t^2
$$
$$
\theta_t = \theta_{t-1} - \frac{\alpha}{\sqrt{G_t} + \epsilon}\, g_t
$$

where:
- $t$ is the current time step / iteration index
- $g_t$ is the gradient of the loss w.r.t. parameter $\theta$ at step $t$
- $G_t$ is the running sum of squared gradients (accumulated from $t=1$)
- $\theta_t$ is the parameter vector being updated
- $\alpha$ is the global learning rate
- $\epsilon$ is a small constant for numerical stability (avoids division by zero)

## Properties
- **No manual learning rate tuning** per parameter — adaptation is automatic
- Works well for **sparse data**: infrequent features accumulate small $G_t$, so their learning rate stays high
- **Weakness: monotonically decreasing learning rate** — $G_t$ only grows, so the effective learning rate shrinks to zero and training stalls
	- [[vanishing learning rate problem]]
	- This motivates [[RMSProp]] (exponential moving average instead of cumulative sum) and [[Adam]]
