---
tags:
  - ml_ai
  - ml_ai/neural_nets
created:
modified: 2026-09-06T10:24
published:
sources:
  - "[TowardsDatascience](https://towardsdatascience.com/large-language-models-gpt-1-generative-pre-trained-transformer-7b895f296d3b)"
topics:
  - Transformers
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Transformer Architecture
- [TowardsDatascience](https://towardsdatascience.com/large-language-models-gpt-1-generative-pre-trained-transformer-7b895f296d3b):
> The original Transformer can be decomposed into two parts which are called encoder and decoder. As the name suggests, the goal of the encoder is to encode an input sequence in the form of a vector of numbers — a low-level format that is understood by machines. On the other hand, the decoder takes the encoded sequence and by applying a language modeling task, it generates a new sequence.
> 
> Encoders and decoders can be used individually for specific tasks. The two most famous models deriving their parts from the original Transformer are called [[BERT]] (Bidirectional Encoder Representations from Transformer) consisting of encoder blocks and [[GPT]] (Generative Pre-Trained Transformer) composed of decoder blocks.
## Topics
- [[Large Language Models]]
- [[Architecture Components]]
- Best visualization of modern LLMs 
	- https://bbycroft.net/llm
## Improved Architectures
- [[Mixture of Experts]]
- [[State Space Models (SSM)]]
- [[Recursive Reasoning with Tiny Networks]]
	- Paper: [Less is More: Recursive Reasoning with Tiny Networks](https://arxiv.org/abs/2510.04618?utm_source=substack&utm_medium=email)
	- TRM simplifies recursive reasoning by using just one tiny network with only two layers, eliminating the need for Hierarchical Reasoning Model's (HRM) hierarchical structure and fixed-point theorems. Instead of assuming convergence to a fixed point for gradient calculations, TRM backpropagates through the entire recursion process.
- [[Loop Transformers]]
	- Recurrent-depth architectures that do test-time compute by looping layers instead of generating tokens
## Additional Concepts
- [[Transformers Caching]]

- Source: ?
![[transformer.png]]

- Source: [Understanding Attention Mechanism, Self-Attention Mechanism and Multi-Head Self-Attention Mechanism](https://medium.com/@limbusapna3/understanding-attention-mechanism-self-attention-mechanism-and-multi-head-self-attention-mechanism-94d14e937820)
![[understand_attention.png]]