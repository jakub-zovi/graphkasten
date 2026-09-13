---
tags:
  - cs
  - cs/databases
created: 2026-06-26T09:53
modified: 2026-09-05T20:34
published:
sources:
  - https://superlinked.com/docs/encode/multivector
topics:
  - Multi-Vector Retrieval
  - ColBERT
  - MUVERA
  - Late Interaction
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Multi-Vector Retrieval
- The multi-vector search can be used for special use cases when an entity within the database is represented by multiple vectors. An example of this can be a house listing that is represented by multiple pictures. You can then represent this house listing with multiple vectors (embeddings of pictures) and increase the chance of finding it when performing the search.
- This operation might seem quite exotic, but it is already being used in RAG applications. We can use this search operator to take advantage of late embedding with Contextualized Late Interaction over BERT [(ColBERT)](https://arxiv.org/pdf/2004.12832). This embedding approach can be used as a reranker [(Vespa ColBert Reranking)](https://blog.vespa.ai/pretrained-transformer-language-models-for-search-part-3/) or as a default embedding. Using Colbert can drastically improve the quality of search at the cost of search time.
- 💡Multi-vector can be employed with [ColBERT](https://arxiv.org/pdf/2004.12832) to perform reranking or with the [ColBERT](https://arxiv.org/pdf/2004.12832) as default embedding to improve the search quality at the cost of search speed.
## List
- [[MUVERA]] (Multi-Vector Retrieval with Approximation)
- [[PLAID]]
	- [PLAID: An Efficient Engine for Late Interaction Retrieval](https://arxiv.org/abs/2205.09707)
- [[GEM]] ([Link](https://arxiv.org/abs/2603.20336))
	- 0 citations
	- 2026-03-26
	- Graph-based index natively designed for multi-vector (Chamfer/MaxSim) retrieval; decouples graph construction (EMD) from search (Chamfer), injects semantic shortcuts, and achieves up to 16x speedup over PLAID/DESSERT/MUVERA
## Storage Considerations

Multi-vector embeddings are significantly larger than dense embeddings because they store one vector per token rather than a single pooled vector:

| Representation | Dimensions | Storage per 1M docs (float32) |
| --- | --- | --- |
| Dense (bge-m3) | 1024 | ~4 GB |
| Multi-vector (ColBERT 128-dim) | ~100 tokens x 128 dim | ~51 GB |
| Multi-vector (ColBERT 96-dim) | ~100 tokens x 96 dim | ~38 GB |
| MUVERA FDE | 10240 | ~41 GB |

The multi-vector storage calculation: 1M docs x 100 tokens x 128 dims x 4 bytes = ~51 GB. Actual token counts vary by document length (max 512 for most models, 8192 for long-context models).

## Multi-Vector Models

| Model                                   | Token Dim | Max Length | Notes                           |
| --------------------------------------- | --------- | ---------- | ------------------------------- |
| `jinaai/jina-colbert-v2`                | 128       | 8192       | Long context, rotary embeddings |
| `answerdotai/answerai-colbert-small-v1` | 96        | 512        | Smallest, fastest               |
| `colbert-ir/colbertv2.0`                | 128       | 512        | Original ColBERT                |
| `mixedbread-ai/mxbai-colbert-large-v1`  | 128       | 512        | Large model, standard dim       |
| `lightonai/GTE-ModernColBERT-v1`        | 128       | 8192       | ModernBERT architecture         |