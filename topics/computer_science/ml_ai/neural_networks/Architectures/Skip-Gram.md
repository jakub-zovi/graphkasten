---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-11-29T10:53
modified: 2026-02-15T11:03
published:
sources:
  - "[Word2Vec (CBOW, Skip-gram) In Depth](https://medium.com/@fraidoonomarzai99/word2vec-cbow-skip-gram-in-depth-88d9cc340a50)"
topics:
  - Word2Vec
authors:
ai-assisted:
hidden:
public: true
---
# Skip-Gram
- Predict the surrounding context words given a target word.
- The model takes the target word and tries to predict each of the context words within a window.
- Performs better on smaller datasets and can capture more complex relationships between words.

<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*w9PeYT8SCN-sIsS4cAqn-Q.png"/>