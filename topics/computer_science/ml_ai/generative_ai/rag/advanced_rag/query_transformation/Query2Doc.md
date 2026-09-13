---
tags:
  - gen_ai
  - gen_ai/rag
created: 2024-12-13T00:16
modified: 2025-08-09T14:35
published:
sources:
  - "[Query2doc: Query Expansion with Large Language Models](https://arxiv.org/pdf/2303.07678)"
topics:
  - Query2Doc
  - Query Expansion
  - Hypothetical Documents
authors:
ai-assisted:
hidden:
public: true
---
# Query2Doc
Good summary of this method [The Geometry of Queries: Query-Based Innovations in Retrieval-Augmented Generation:](https://arxiv.org/pdf/2407.18044)
> **Query2Doc**. Similarly to [[HyDE]], Query2Doc employs few-shot prompting to generate a hypothetical pseudo-document that would answer the query. It concatenates the initial query with the synthetic document (generated similar to HyDE) and then performs dense retrieval using the embeddings of this concatenated text. Given the similarity with HyDE, we only implement HyDE in our benchmark.