---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-06-28T11:55
modified: 2026-06-28T11:57
published:
sources:
topics:
  - Learned Sparse Retrieval
  - SPLADE
  - Sparse Embeddings
  - BGE M3
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Learned Sparse Retrieval
- [AI Summary From Wiki](https://en.wikipedia.org/wiki/Learned_sparse_retrieval)
> Learned Sparse Retrieval (LSR) is an information retrieval paradigm that uses neural networks to map queries and documents into high-dimensional, sparse vectors. It combines the deep semantic understanding of neural embeddings with the efficiency and transparency of traditional keyword-based search. 
## List
- [[SPLADE]]
	- Transformer-based model that outputs sparse vectors (vocab-weighted) — like “semantic BM25”. Scores come from a neural model trained to activate relevant tokens ([Splade_PP_en_v1](https://huggingface.co/prithivida/Splade_PP_en_v1), [Making Sparse Neural IR Models More Effective](https://arxiv.org/pdf/2205.04733), [SparseEmbed](https://storage.googleapis.com/gweb-research2023-media/pubtools/pdf/79f16d3b3b948706d191a7fe6dd02abe516f5564.pdf)).
- [[SPLARE]] ([Link](https://arxiv.org/abs/2603.13277))
	- LSR approach from NAVER that replaces vocabulary-space projection with representations from pre-trained Sparse Autoencoders (SAEs) — making it monosemantic, language-agnostic, and scalable ([arxiv](https://arxiv.org/abs/2603.13277))
	- Best LSR model on MMTEB (Multilingual, v2); uses frozen Llama Scope SAE + SPLADE-style max-pooling + LoRA fine-tuning
- [[BGE M3]]
	- Has capabilities in Multi-Linguality, Multi-Functionality, and Multi-Granularity. Capable of supporting over 100 languages, BGE-M3 and supports dense retrieval, multi-vector retrieval, and sparse retrieval within a single framework makes it an ideal choice for a wide range of information retrieval (IR) applications ([Source](https://milvus.io/docs/embed-with-bgm-m3.md)).
	- TODO: miniCOIL: on the Road to Usable Sparse Neural Retrieval