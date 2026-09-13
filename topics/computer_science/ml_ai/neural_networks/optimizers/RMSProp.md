---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/optimizers
created: 2026-03-09T10:00
modified: 2026-07-26T13:31
published:
sources:
  - "[Lecture 6e — rmsprop: Divide the gradient by a running average of its recent magnitude (Hinton, 2012)](https://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf)"
topics:
  - Optimizers
  - Adaptive Learning Rate
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# RMSProp
RMSProp (Root Mean Square Propagation) fixes the vanishing learning rate problem of [AdaGrad](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FAdaGrad) by replacing the cumulative sum of squared gradients with an exponential moving average. Proposed by Hinton in his Coursera lecture (2012).

## Motivation
- [AdaGrad](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FAdaGrad) accumulates all past squared gradients, causing the effective learning rate to decrease monotonically toward zero
- RMSProp [[discounts older gradients via exponential decay]], keeping the learning rate from collapsing

## Update Rule
$$
v_t = \rho\, v_{t-1} + (1 - \rho)\, g_t^2
$$
$$
\theta_t = \theta_{t-1} - \frac{\alpha}{\sqrt{v_t} + \epsilon}\, g_t
$$

where:
- $t$ is the current time step / iteration index
- $g_t$ is the gradient of the loss w.r.t. parameter $\theta$ at step $t$
- $v_t$ is the exponential moving average of squared gradients
- $\theta_t$ is the parameter vector being updated
- $\rho \approx 0.9$ is the decay rate (controls how quickly past gradients are forgotten)
- $\alpha$ is the learning rate
- $\epsilon$ is a small constant for numerical stability (avoids division by zero)

## Properties
- Effective learning rate is stabilized — does not monotonically decrease
- Works well in non-stationary settings (RNNs, online learning)
- Does not include bias correction (unlike [[Adam]])
- [[Adam]] can be seen as RMSProp + momentum + bias correction
