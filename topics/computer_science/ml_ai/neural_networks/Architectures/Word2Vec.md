---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-11-29T10:50
modified: 2026-02-15T11:03
published:
sources:
  - "[Word2Vec (CBOW, Skip-gram) In Depth](https://medium.com/@fraidoonomarzai99/word2vec-cbow-skip-gram-in-depth-88d9cc340a50), [Fast Similarity Searching of Text Documents Using Learned Metric Index](https://is.muni.cz/auth/th/wmtet/Fast_Similarity_Searching_of_Text_Documents_using_Learned_Metric_Index.pdf)"
topics:
  - Word2Vec
authors:
ai-assisted:
hidden:
public: true
---
# Word2Vec
The first shallow window method for the computation of word embeddings is Word2Vec. This method creates static embeddings, which means there is always one embedding for each word in the vocabulary.

Word2Vec has two main architectures for generating word embeddings:
1. [[Continuous Bag-of-Words (CBOW)]]
2. [[Skip-Gram]]
