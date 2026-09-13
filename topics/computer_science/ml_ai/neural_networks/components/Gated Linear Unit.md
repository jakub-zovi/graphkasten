---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-10-14T09:47
modified: 2026-02-15T11:01
published:
sources:
  - "[Language Modeling with Gated Convolutional Networks](https://arxiv.org/abs/1612.08083)"
topics:
  - Gated Linear Unit
  - Gating Mechanism
  - Activation Functions
authors:
ai-assisted:
hidden:
public: true
---
# Gated Linear Unit (GLU)
One of the papers that first presents GLU is [Language Modeling with Gated Convolutional Networks](https://arxiv.org/abs/1612.08083). A **Gated Linear Unit** introduces a gating mechanism that regulates how much information passes through a layer. This mechanism helps the network learn which parts of the input are important and which can be suppressed, adding flexibility to the model. It’s inspired by the idea of the gates of [[LSTM]]s, but applied to convolutions and linear layers, but it’s the same idea.

GLU splits the input into two parts:
1. The first part is transformed in a linear manner.
2. The second part is passed through a gate, which modulates (controls) the flow of information from the first part.

Mathematically, GLU can be expressed as:
$$
\text{Output} = (W \cdot X_1 + b_1) \times \sigma(W' \cdot X_2 + b_2)
$$

Where:
- $X_1$ and $X_2$ are two parts of the input $X$,
- $W$ and $W'$ are weight matrices,
- $b_1$ and $b_2$ are biases,
- $\sigma$ is the sigmoid function, which serves as the gating function.
- The sigmoid output controls the flow of information by multiplying it element-wise with the linear transformation of the first part.
