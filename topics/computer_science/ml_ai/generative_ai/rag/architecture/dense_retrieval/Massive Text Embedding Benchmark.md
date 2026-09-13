---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-07-07T10:00
modified: 2026-08-01T11:07
published: 2022-10-13
sources:
  - "[MTEB Embedding Leaderboard](https://huggingface.co/spaces/mteb/leaderboard)"
  - "[MTEB: Massive Text Embedding Benchmark](https://arxiv.org/abs/2210.07316)"
  - "[MMTEB: Massive Multilingual Text Embedding Benchmark](https://arxiv.org/abs/2502.13595)"
topics:
  - Embedding Evaluation
  - Retrieval Benchmarks
authors:
  - Opus 4.7
ai-assisted: true
hidden: false
public: true
human-review: true
---
# Massive Text Embedding Benchmark
- MTEB is the de-facto public benchmark for comparing text embedding models across a broad set of downstream tasks.
- Hosted as a HuggingFace Space by the `mteb` organization: [MTEB Leaderboard](https://huggingface.co/spaces/mteb/leaderboard)
- Originally introduced to address the fact that ([MTEB Paper](https://arxiv.org/abs/2210.07316)):
> no particular text embedding method dominates across all tasks
- Parent note: [[Embedding Leaderboards]]
## Task Categories
- Semantic Textual Similarity (STS)
- Retrieval
- Reranking
- Classification
- Pair Classification
- Clustering
- Summarization
- Bitext Mining
## Original MTEB (v1)
- Paper: [MTEB: Massive Text Embedding Benchmark](https://arxiv.org/abs/2210.07316)
	- Authors: Niklas Muennighoff, Nouamane Tazi, Loïc Magne, Nils Reimers
	- 2022-10-13 (v1), 2023-03-19 (v3)
	- 8 task categories, 58 datasets, 112 languages, 33 models at release
## MMTEB — Multilingual Extension
- Paper: [MMTEB: Massive Multilingual Text Embedding Benchmark](https://arxiv.org/abs/2502.13595)
	- Lead author: Kenneth Enevoldsen (+ 84 co-authors, community-driven)
	- 2025-02-19 (v1), 2025-11-13 (v4) — accepted at ICLR
	- 500+ quality-controlled evaluation tasks across 250+ languages
	- Adds novel task types: instruction following, long-document retrieval, code retrieval
	- Introduces downsampling based on inter-task correlation to reduce compute while preserving model rankings
- Notable finding: `multilingual-e5-large-instruct` (560M params) outperformed much larger LLMs on the benchmark.
