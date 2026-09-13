---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-04-03T08:54
modified: 2026-07-04T15:27
published:
sources:
  - "[What is the difference between sparse and dense retrieval?](https://milvus.io/ai-quick-reference/what-is-the-difference-between-sparse-and-dense-retrieval)"
topics:
  - Dense Retrieval
  - Bi-Encoder
  - Embeddings
authors:
ai-assisted:
hidden:
public: true
---
# Dense Retrieval (Bi-Encoder)
[What is the difference between sparse and dense retrieval?](https://milvus.io/ai-quick-reference/what-is-the-difference-between-sparse-and-dense-retrieval):
> Dense retrieval, on the other hand, uses neural networks to map text into lower-dimensional, continuous vectors (embeddings) that capture semantic meaning. These vectors are “dense” because every dimension contains a non-zero value, allowing similarities to be measured even when the exact keywords don’t match

Encoder or embedding model is used to transforms text chunks into a vector representation upon which the search is performed. This note aggregates more practical rather than theoretical knowledge related to encoders. For theoretical information see [BERT](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2FArchitectures%2FBERT) and [Transformers](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2FArchitectures%2FTransformer).
## Resources
- [[Embedding Serving]]
- [[Bi-Encoder Fine-tuning]]
- [[Encoder Libraries]]
- [[Embedding Leaderboards]]
## Papers
- [ON THE THEORETICAL LIMITATIONS OF EMBEDDING-BASED RETRIEVAL](https://arxiv.org/pdf/2508.21038)
	- 2026-03-12
	- 50 citations
- [[The Universal Weight Subspace Hypothesis]]
	- 8 citations
	- 2025-12-04
## Models
- [[Zembed-1]]
	- 2026-08-05 — ZeroEntropy 4B multilingual embedding model, distilled from zerank-2 via zELO methodology, tops proprietary models (OpenAI large, Cohere v4, gemini-embed-001, voyage-4-nano) on their benchmark
## Blogs
- [[Recent Trends with Text Embeddings Decoder-Only LLMs]] ([Link](https://yuvalmerhav.com/posts/2024-12-02-decoder-embeddings/))
	- 2024-12-02 — reviews E5-Mistral, NV-Embed, GritLM, LLM2Vec and the decoder-only shift on the MTEB leaderboard