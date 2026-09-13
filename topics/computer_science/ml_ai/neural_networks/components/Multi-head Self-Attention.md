---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-10-13T22:15
modified: 2026-07-26T13:35
published:
sources:
  - "PV021 Neural Networks"
topics:
  - Self-Attention
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Multi-head Self-Attention
An extension of self-attention where multiple attention heads compute attention scores in parallel on different learned projections of the input, capturing diverse contextual information before concatenating and projecting them back into the original dimension.
## Detailed Description
Assume the number of **heads** is $H$.
For $h = 1, \dots, H$, the $h$-th head is an attention mechanism which, given the input $\vec{x}_1, \dots, \vec{x}_T$, produces:
$$ \vec{y}_1^h, \dots, \vec{y}_T^h $$
**Note:** The output may be different, which means that, in particular, the matrices $W_q, W_k, W_v$ may be different for each head.
Assume that all vectors $\vec{y}_k^h$ are of the same dimension $d_{mid}$, and consider a learnable matrix $W_{out}$ of dimensions $d_{out} \times (H \cdot d_{mid})$.
The multi-head attention produces the following output:
$$ \vec{y}_1, \dots, \vec{y}_T $$
where:
$$ \vec{y}_k = W_{out} \cdot (\vec{y}_k^1 \circ \vec{y}_k^2 \circ \dots \circ \vec{y}_k^H) $$
Here $\circ$ denotes concatenation of vectors.
## Summary
**Input:** A sequence $\vec{x}_1, \dots, \vec{x}_T$
**Output:** A sequence $\vec{y}_1, \dots, \vec{y}_T$
I.e., a sequence of the same length. The dimensions of $\vec{y}_k$ and $\vec{x}_k$ do not have to be equal.

---
### Attention:
**Learnable parameters:** Matrices $W_q, W_k, W_v$.
These matrices are used to compute queries, keys, and values from $\vec{x}_1, \dots, \vec{x}_T$. Output $\vec{y}_1, \dots, \vec{y}_T$ is computed using values "scaled" by the query-key attention.

---
### Multi-head attention:
**Learnable parameters:**
- Matrices $W_q^h, W_k^h, W_v^h$ where $h = 1, \dots, H$ and $H$ is the number of heads.
    Each attention head operates independently on the input $\vec{x}_1, \dots, \vec{x}_T$.
- Matrix $W_{out}$.
    Linearly transforms the concatenated results of the attention heads.

## Intuition
- **Single head limitation** — one set of $W_q, W_k, W_v$ can encode only one "perspective" on token relationships at a time; a sentence has many simultaneous relationship types (syntactic agreement, coreference, positional proximity, semantic similarity) that a single head cannot capture in parallel
- **Parallel specialisation** — each head $h$ gets its own independent projections $W_q^h, W_k^h, W_v^h$, so through training the heads naturally specialise on different aspects of the input without being explicitly told to
	- e.g. one head may learn to resolve coreference ("it" → "the cat"), another may track subject-verb agreement, another may attend to nearby tokens for local context
- **Concatenation + $W_{out}$** — stacking all head outputs and projecting with a learned $W_{out}$ lets the model decide *how much weight* to give each head's perspective rather than averaging them blindly; the projection also brings the dimension back to $d_{out}$
- **No extra sequential cost** — all $H$ heads run in parallel on the same input sequence, so the wall-clock cost is comparable to a single wide head; the benefit is richer representations at roughly the same depth
- **Analogy** — like consulting $H$ domain experts simultaneously, each studying the same text through a different lens, then having a manager ($W_{out}$) synthesise their reports into one coherent answer
