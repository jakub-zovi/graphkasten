---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2026-05-23T15:50
modified: 2026-07-26T13:37
published:
sources:
topics:
  - Neural Networks
  - Activation Functions
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
---
# Logit
The **raw, unnormalized output** of a neural network's final linear layer — the values fed into [[Softmax]] or [[Sigmoid]] to produce probabilities. Logits live in $(-\infty, +\infty)$ and carry the model's pre-activation evidence for each class.
## Statistical Definition
In statistics, the logit is the inverse of the [[Sigmoid]] (logistic) function — the **log-odds** of a probability $p \in (0, 1)$:
$$
\text{logit}(p) = \ln\!\left(\frac{p}{1 - p}\right)
$$

- Maps probabilities from $(0, 1)$ to $(-\infty, +\infty)$
- $\text{logit}(0.5) = 0$, $\text{logit}(p) > 0$ when $p > 0.5$, and $\text{logit}(p) < 0$ when $p < 0.5$
- Inverse relationship: $\sigma(\text{logit}(p)) = p$
## In Neural Networks
For a final linear layer with weights $W$ and bias $b$ acting on hidden representation $h$:
$$
z = W h + b
$$
The vector $z \in \mathbb{R}^K$ is called the **logits**. It is converted to a probability distribution via:
- [[Sigmoid]] for binary classification: $p = \sigma(z)$
- [[Softmax]] for multi-class classification: $p_i = \frac{e^{z_i}}{\sum_j e^{z_j}}$

Key properties:
- **Shift invariance under softmax** — adding a constant $c$ to every logit leaves the softmax output unchanged, which is why subtracting $\max(z)$ is a safe numerical stabilization trick
- **Scale sensitivity** — multiplying logits by a temperature $T$ sharpens ($T < 1$) or smooths ($T > 1$) the resulting distribution
- **Loss computation** — [[Cross-Entropy]] is typically computed directly from logits (e.g. `nn.CrossEntropyLoss` in PyTorch) for numerical stability, fusing the log-softmax and NLL steps
## Logit Manipulation Use Cases
- **Temperature scaling** — divide logits by $T$ before softmax to control output entropy (sampling diversity in LLMs)
- **Logit bias / logit masking** — add $-\infty$ to disallowed tokens to forbid them, or positive offsets to favor them (used in Structured Output and constrained decoding)
- **Calibration** — post-hoc temperature scaling on logits to align model confidence with empirical accuracy
- **Knowledge distillation** — student models are trained to match teacher logits (softened with temperature) rather than hard labels
