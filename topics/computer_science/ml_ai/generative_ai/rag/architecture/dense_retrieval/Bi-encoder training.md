---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-08-19T07:50
modified: 2026-03-22T18:59
published:
sources:
topics:
  - Bi-Encoder
  - Contrastive Learning
  - InfoNCE
  - Metric Learning
authors:
ai-assisted:
hidden:
public: true
---
# Bi-encoder training
(Source: ChatGPT5[^1])
You're right that in a **cross-encoder**, it's easy to see how the error is propagated: the model jointly encodes $(q,d)$ into one forward pass, produces a similarity score (or classification probability), and directly backpropagates the loss.

The **bi-encoder** case feels more mysterious because query and document are processed separately, and the network never literally "sees them together" before the similarity computation. But the key is:

---

## 1. Architecture Recap

A **bi-encoder** has two encoders:

* $f_\theta(q) \to \mathbf{q} \in \mathbb{R}^d$
* $g_\theta(d) \to \mathbf{d} \in \mathbb{R}^d$

In many cases, $f$ and $g$ share weights ($f=g$), but they don't have to.

Similarity is computed via some differentiable function $s(\mathbf{q},\mathbf{d})$, often:

$$
s(\mathbf{q},\mathbf{d}) = \cos(\mathbf{q},\mathbf{d}) \quad \text{or} \quad s(\mathbf{q},\mathbf{d}) = \mathbf{q}^\top \mathbf{d}
$$

---

## 2. Training Objective

The bi-encoder is typically trained with **pairwise** or **contrastive** loss functions.
Two common ones:

### a. Binary classification loss (pairwise)

Given $(q,d^+)$ as a positive pair and $(q,d^-)$ as a negative pair, the loss could be:

$$
\mathcal{L} = - \log \sigma(s(\mathbf{q}, \mathbf{d}^+)) - \log (1 - \sigma(s(\mathbf{q}, \mathbf{d}^-)))
$$

Here, $s(\mathbf{q},\mathbf{d})$ is differentiable w.r.t. both $\mathbf{q}$ and $\mathbf{d}$.

---

### b. Softmax-based contrastive loss (InfoNCE)

With a batch of $B$ positive pairs $(q_i,d_i)$, treat all other $d_j, j \neq i$ as negatives:

$$
\mathcal{L} = -\frac{1}{B} \sum_{i=1}^B \log \frac{\exp(s(\mathbf{q}_i, \mathbf{d}_i) / \tau)}{\sum_{j=1}^B \exp(s(\mathbf{q}_i, \mathbf{d}_j) / \tau)}
$$

---

## 3. How the Error Propagates

Let's say $s(\mathbf{q},\mathbf{d}) = \mathbf{q}^\top \mathbf{d}$.

For a single pair $(q,d)$:

$$
\frac{\partial s}{\partial \mathbf{q}} = \mathbf{d} \quad \text{and} \quad \frac{\partial s}{\partial \mathbf{d}} = \mathbf{q}
$$

Now, apply the chain rule through the loss:

1. **Forward pass**:

   * Encode $q \to \mathbf{q}$
   * Encode $d \to \mathbf{d}$
   * Compute score $s(\mathbf{q},\mathbf{d})$
   * Compute loss $\mathcal{L}$

2. **Backward pass**:

   * Loss gives $\frac{\partial \mathcal{L}}{\partial s}$
   * That flows into $\frac{\partial s}{\partial \mathbf{q}}$ and $\frac{\partial s}{\partial \mathbf{d}}$
   * Then into each encoder separately:

     $$
     \frac{\partial \mathcal{L}}{\partial \theta_q} = \frac{\partial \mathcal{L}}{\partial \mathbf{q}} \cdot \frac{\partial \mathbf{q}}{\partial \theta_q}
     $$

     $$
     \frac{\partial \mathcal{L}}{\partial \theta_d} = \frac{\partial \mathcal{L}}{\partial \mathbf{d}} \cdot \frac{\partial \mathbf{d}}{\partial \theta_d}
     $$
   * If weights are shared, the gradients from both flows are summed before updating.

---

## 4. Why This Works Without Joint Encoding

The model **doesn't** see the pair concatenated, but it **does** receive a gradient signal for:

* **Pushing** query and positive doc vectors closer (higher dot product / cosine)
* **Pulling apart** query and negative doc vectors

This is essentially **metric learning**:
The encoders learn embeddings such that semantically similar texts live nearby in vector space.

The cross-encoder optimizes **direct classification**; the bi-encoder optimizes **representation space geometry**.

---

## 5. Example in Pseudocode (PyTorch)

```python
import torch
import torch.nn as nn
import torch.nn.functional as F

encoder = MyBERTEncoder()  # shared for q and d

def bi_encoder_loss(q_inputs, d_inputs, temperature=0.05):
    q_vecs = encoder(q_inputs)     # (B, d)
    d_vecs = encoder(d_inputs)     # (B, d)
    logits = q_vecs @ d_vecs.T / temperature  # (B, B)
    labels = torch.arange(len(q_vecs)).to(logits.device)
    loss = F.cross_entropy(logits, labels)
    return loss
```

Here:

* `logits[i, j]` = similarity between $q_i$ and $d_j$
* Gradient flows from `loss` → `logits` → both `q_vecs` and `d_vecs` → encoder weights.

[^1]: Prompts: "How is the bi-encoder fine-tuned to align it to produce correct similarity scores? I understand it for the cross-encoder since the model sees both the query and the document. I do not understand how is the error propagated in the bi-ecnoder. I am CS graduate so you can be technical.", "Same output but fixed the mathematical notations with $ dollar sign without spaces around so it renders in my markdown."
