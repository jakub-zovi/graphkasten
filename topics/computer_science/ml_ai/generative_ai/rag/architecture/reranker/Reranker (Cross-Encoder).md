---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-03-22T19:00
modified: 2026-08-01T11:09
published:
sources:
  - "[Cross-Encoders — Sentence Transformers](https://sbert.net/examples/applications/cross-encoder/README.html)"
  - "[cross-encoder/ms-marco-MiniLM-L-6-v2 — HuggingFace](https://huggingface.co/cross-encoder/ms-marco-MiniLM-L-6-v2)"
topics:
  - Cross-Encoder
  - Reranking
  - RAG
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Reranker (Cross-Encoder)
- A cross-encoder is a model that takes a **query–document pair as a single concatenated input** and outputs a scalar relevance score
- Contrast with a bi-encoder, which encodes query and document independently

![|500](Bi_vs_Cross-Encoder.png)

## Topics
- [[Reranker Models]]
- [[Cross-Encoder Training]]
	- Sentence Trasformers
## Architecture
- Input: `[CLS] query [SEP] document [SEP]` — both texts concatenated and passed through the encoder together
- Backbone: transformer encoder (BERT, RoBERTa, MiniLM)
- Head: linear layer on the `[CLS]` token → scalar logit (or softmax for classification)
- The model attends across both query and document tokens — full cross-attention
- No vector index can be built; the score must be computed fresh for every (query, doc) pair at inference

## Bi-Encoder vs Cross-Encoder

|                           | Bi-Encoder                        | Cross-Encoder               |
| ------------------------- | --------------------------------- | --------------------------- |
| Input                     | query and doc encoded separately  | query + doc concatenated    |
| Speed                     | fast (pre-compute doc embeddings) | slow (re-encode every pair) |
| Accuracy                  | lower                             | higher                      |
| Scalable to large corpora | yes                               | no                          |
| Used for                  | retrieval                         | reranking                   |

## Papers
- [[Beyond the Reranker]]
	- 2026-07-03 — once a strong cross-encoder reranker is present, only HyDE query expansion and per-source calibration (SSCC) give reliable gains on heterogeneous corpora
