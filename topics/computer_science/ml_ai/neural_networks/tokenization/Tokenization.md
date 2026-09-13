---
tags:
  - ml_ai
  - ml_ai/neural_nets
created:
modified: 2026-07-18T16:33
published:
sources:
  - "[All you need to know about Tokenization in LLMs](https://medium.com/thedeephub/all-you-need-to-know-about-tokenization-in-llms-7a801302cf54)"
topics:
  - Tokenization
authors:
ai-assisted:
hidden:
public: true
---
# Tokenization
Tokenization is the process of converting text into a sequence of tokens, which can be words, subwords, or characters. These tokens are the smallest units of meaning in a text that can be processed by a language model. For example, the sentence “Hello, world!” can be tokenized into ,[“Hello”, “,”, “world”, “!”]. Tokenization simplifies the text and allows the model to work with manageable chunks of data.

In the LLM pre-training and inference workflows, after the tokenization, each token is assigned a unique integer. For each integer, there is a corresponding row in a lookup table, which is the vector representation of that token. This vector is then used as input for a particular token in the language model.
## List Of Approaches
- [[Byte-pair encoding]]
- [[WordPiece]]
- [[Byte-Level]]