---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/optimizers
created: 2026-03-09T10:00
modified: 2026-07-26T13:32
published:
sources:
  - "[Adam: A Method for Stochastic Optimization](https://arxiv.org/abs/1412.6980)"
topics:
  - Optimizers
  - Adaptive Learning Rate
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Adam
Adam (Adaptive Moment Estimation) is a first-order gradient-based optimization algorithm that combines the benefits of [AdaGrad](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FAdaGrad) (per-parameter adaptive learning rates) and [RMSProp](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FRMSProp) (exponential moving average of squared gradients). Introduced by Kingma & Ba (2014).

## Key Idea
- Maintains two moving averages of gradients:
	- **First moment** $m_t$ — mean of gradients (like momentum)
	- **Second moment** $v_t$ — uncentered variance of gradients (like RMSProp)
- Both are bias-corrected to account for zero-initialization

## Update Rule
$$
m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t
$$
$$
v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2
$$
$$
\hat{m}_t = \frac{m_t}{1 - \beta_1^t}, \quad \hat{v}_t = \frac{v_t}{1 - \beta_2^t}
$$
$$
\theta_t = \theta_{t-1} - \frac{\alpha}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t
$$

where:
- $t$ is the current time step / iteration index
- $g_t$ is the gradient of the loss w.r.t. parameter $\theta$ at step $t$
- $m_t$ is the first moment — exponential moving average of gradients (tracks direction)
- $v_t$ is the second moment — exponential moving average of squared gradients (tracks magnitude)
- $\hat{m}_t$ is the bias-corrected first moment estimate
- $\hat{v}_t$ is the bias-corrected second moment estimate
- $\beta_1 \approx 0.9$ is the decay rate for the first moment
- $\beta_2 \approx 0.999$ is the decay rate for the second moment
- $\beta_1^t$, $\beta_2^t$ are the decay rates raised to the power of $t$ (used for bias correction)
- $\theta_t$ is the parameter vector being updated
- $\alpha$ is the learning rate
- $\epsilon$ is a small constant for numerical stability (avoids division by zero)

## Bias Correction
- At initialization $m_0 = v_0 = 0$, so early estimates are biased toward zero
- Dividing by $(1 - \beta^t)$ corrects this — the correction decays to 1 as $t \to \infty$

## Properties
- Adaptive per-parameter learning rates — handles sparse and dense gradients well
- Computationally efficient — $O(n)$ memory and time per step
- Default hyperparameters work well across a wide range of tasks
- L2 regularization in Adam is **not** equivalent to weight decay — see [[Adamw]]
