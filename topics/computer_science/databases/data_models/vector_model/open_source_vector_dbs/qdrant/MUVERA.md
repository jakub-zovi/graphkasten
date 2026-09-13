---
tags:
  - cs
  - cs/databases
created: 2026-07-02T16:06
modified: 2026-07-06T09:52
published:
sources:
  - "[MUVERA: Multi-Vector Retrieval via Fixed Dimensional Encodings](https://arxiv.org/abs/2405.19504)"
topics:
  - MUVERA
  - Multi-Vector Retrieval
  - Fixed Dimensional Encodings
  - MIPS
authors:
  - Jakub
ai-assisted:
hidden:
public: true
banner: https://storage.googleapis.com/gweb-research2023-media/original_images/MUVERA_Cover.png
banner-x: 51
banner-y: 41
---
# MUVERA
- [MUVERA: Multi-Vector Retrieval via Fixed Dimensional Encodings](https://arxiv.org/abs/2405.19504):
> MUVERA (MUlti-VEctor Retrieval Algorithm), a retrieval mechanism which reduces multi-vector similarity search to single-vector similarity search. This enables the usage of off-the-shelf MIPS solvers for multi-vector retrieval. MUVERA asymmetrically generates Fixed Dimensional Encodings (FDEs) of queries and documents, which are vectors whose inner product approximates multi-vector similarity. We prove that FDEs give high-quality ϵ-approximations, thus providing the first single-vector proxy for multi-vector similarity with theoretical guarantees. Empirically, we find that FDEs achieve the same recall as prior state-of-the-art heuristics while retrieving 2-5× fewer candidates. Compared to prior state of the art implementations, MUVERA achieves consistently good end-to-end recall and latency across a diverse set of the BEIR retrieval datasets, achieving an average of 10% improved recall with 90% lower latency.
## Resources
- [sionic-ai/muvera-py](https://github.com/sionic-ai/muvera-py)
	- Python Implementation of MUVERA (Multi-Vector Retrieval via Fixed Dimensional Encodings)
- [[MUVERA Making multi-vector retrieval as fast as single-vector search]] ([Link](https://research.google/blog/muvera-making-multi-vector-retrieval-as-fast-as-single-vector-search/))
	- 2025-06-25
	- Google Research announcement of MUVERA and FDEs
- [[MUVERA Making Multivectors More Performant]] ([Link](https://qdrant.tech/articles/muvera-embeddings/))
	- 2025-09-05
- [[MUVERA - Qdrant Course]]