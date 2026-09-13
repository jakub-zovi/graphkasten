---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-10-16T11:48
modified: 2026-06-08T10:00
published:
sources:
topics:
  - Benchmarks
authors:
ai-assisted:
hidden:
public: true
---
# RAG Benchmarks
- This note aggregates information about benchmarks that can be used to measure performance of RAG systems. There can be slight overlap between agentic and rag benchmarks.
## List
- [[RAGBench]]: Explainable Benchmark for Retrieval-Augmented Generation Systems
	- This actually benchmarks evaluation of the RAG and no the RAG itself
	- Paper: [RAGBench: Explainable Benchmark for Retrieval-Augmented Generation Systems](https://arxiv.org/pdf/2407.11005)
		- 2025-01-16
		- 87 citations
	- Hugging Face: [galileo-ai/ragbench](https://huggingface.co/datasets/galileo-ai/ragbench)
- [[UNIDOC-BENCH]]
	- A unified benchmark for document-centric multimodal retrieval-augmented generation (MM-RAG). This project provides the first large-scale, realistic benchmark for MM-RAG built from 70k real-world PDF pages across eight domains, with tools for document tagging, dataset synthesis, baseline implementations, and evaluation frameworks.
	- Github: [SalesforceAIResearch/UniDOC-Bench](https://github.com/SalesforceAIResearch/UniDOC-Bench)
		- 10 stars
	- Paper: [UNIDOC-BENCH: A Unified Benchmark for Document-Centric Multimodal RAG](https://arxiv.org/abs/2510.03663)
		- 0 citations
		- Submitted on 2025-10-9
- [[LiveRAG]]: A diverse Q&A dataset with varying difficulty level for RAG evaluation
	- https://arxiv.org/abs/2511.14531
	- https://huggingface.co/datasets/LiveRAG/Benchmark
	- LiveRAG is a benchmark of 895 synthetic question–answer pairs derived from the SIGIR 2025 LiveRAG Challenge, designed to support systematic evaluation of RAG systems. Built using the DataMorgana generation pipeline, it combines questions from two challenge sessions and augments them with reference answers, supporting documents, and the “answer claims” used for evaluation. Each question is also associated with difficulty and discriminability scores. The benchmark spans diverse question types and linguistic variations.
- [[RAGPulse]]: An Open-Source RAG Workload Trace to Optimize RAG Serving Systems
	- https://arxiv.org/abs/2511.12979
	- https://github.com/flashserve/RAGPulse
	- RAGPulse is a dataset collected from a university-wide RAG-based policy Q&A system that has served over 40,000 users since April 2024. The dataset contains 7,106 anonymized request records sampled over one week, capturing system-level information such as timestamps, input and output token lengths, hashed identifiers for all input components, and session metadata.
- [A Benchmark for Conversational Data Retrieval](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fgenerative_ai%2Fagents%2Fevaluation%2FA%20Benchmark%20for%20Conversational%20Data%20Retrieval)
- [[RAGSearch]] ([Link](https://arxiv.org/abs/2604.09666)): Benchmark comparing dense RAG and five GraphRAG variants (GraphRAG, RAPTOR, HippoRAG2, HyperGraphRAG, LinearRAG) as retrieval backends in agentic search systems across general QA and multi-hop datasets
- [[MultiHop-RAG]]: Benchmarking Retrieval-Augmented Generation for Multi-Hop Queries
	- A benchmark dataset built from English news articles, containing a knowledge base, multi-hop queries, ground-truth answers, and supporting evidence. Demonstrates that current SOTA embedding models and LLMs (GPT-4, PaLM, Llama2-70B) perform inadequately on multi-hop QA.
	- Paper: [MultiHop-RAG: Benchmarking Retrieval-Augmented Generation for Multi-Hop Queries](https://arxiv.org/abs/2401.15391)
		- 2024-01-27
	- Github: [yixuantt/MultiHop-RAG](https://github.com/yixuantt/MultiHop-RAG)
		- 449 stars
