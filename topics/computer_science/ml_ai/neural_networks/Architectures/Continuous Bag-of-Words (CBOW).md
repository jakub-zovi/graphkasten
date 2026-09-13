---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-11-29T10:51
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
# Continuous Bag-of-Words (CBOW)
- Predict the target word (center word) from the surrounding context words.
- The model averages the vectors of context words and uses this average to predict the target word.
- Faster to train since it predicts only one word from multiple context words.

<img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*UghCgUf3ADegvMcUrsibmQ.png"/>
<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*4IM6YiGM7LSRu7SBq9tSBA.png"/>