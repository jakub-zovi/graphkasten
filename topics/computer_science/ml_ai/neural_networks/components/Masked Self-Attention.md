---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-10-13T22:10
modified: 2026-02-15T10:11
published:
sources:
  - "PV021 Neural Networks"
topics:
  - Self-Attention
authors:
ai-assisted:
hidden:
public: true
---
# Masked Self-Attention
A variant of self-attention used in autoregressive models (e.g., GPT) where a causal mask is applied to prevent attending to future tokens, ensuring that each position can only attend to past and current positions.
## Detailed Description
Assume an attention mechanism which, given an input sequence  $\vec{x}_1, \ldots, \vec{x}_T$, generates  $\vec{y}_1, \ldots, \vec{y}_T$.
**The Problem**: How to generate  $\vec{y}_k$ only based on  $\vec{x}_1, \ldots, \vec{x}_{k-1}$?

Define a vector score for all  $i, j \in \{ 1, \ldots, T \}$ by:
$$
e_{ij} = 
\begin{cases} 
\vec{q}_i \cdot \vec{k}_j & \text{if } j < i \\
-\infty & \text{otherwise}
\end{cases}
$$
This means that:
$$
\alpha_{ij} = 
\begin{cases} 
\frac{\exp(e_{ij} / \sqrt{d_{attn}})}{\sum_{k=1}^{i-1} \exp(e_{jk} / \sqrt{d_{attn}})} & \text{if } j < i \\
0 & \text{otherwise}
\end{cases}
$$
Define a sequence of outputs  $\vec{y}_1, \ldots, \vec{y}_T$ by:

$$
\vec{y}_i = \sum_{j=1}^{T} \alpha_{ij} \cdot \vec{v}_j
$$
