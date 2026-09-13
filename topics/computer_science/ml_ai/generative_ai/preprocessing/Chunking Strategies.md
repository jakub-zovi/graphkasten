---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-08T11:52
modified: 2026-08-06T08:57
published:
sources:
  - "[Pinecone Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/)"
  - "[Searching for Best Practices in RAG](https://aclanthology.org/2024.emnlp-main.981.pdf)"
  - "[RAG for LLMs: A Survey](https://arxiv.org/pdf/2312.10997)"
topics:
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Chunking Strategies
- [Pinecone Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/):
> There are different methods for chunking, and each of them might be appropriate for different situations. By examining the strengths and weaknesses of each method, our goal is to identify the right scenario to apply them to.
## List
- [[Sliding-window (Fixed-sized) Chunking]]
- [[Recursive Chunking]]
- [[Specialized Chunking]]
- [[Semantic Chunking]]
- [[Small2Big]]
- [[Late Chunking]]
## Evaluations
- [[An evaluation of Retrieval Chunking Methods for Inference Systems]] ([Link](https://superlinked.com/blog/evaluation-retrieval-chunking-methods-for-inference-systems))
	- 2026-04-07 — Superlinked benchmark of LlamaIndex/LangChain chunkers on HotpotQA, SQUAD, QuAC across MTEB embedders and rerankers
- [[Semantic Chunking - Superlinked Blog]] ([Link](https://superlinked.com/blog/semantic-chunking))
	- 2026-04-07 — Superlinked deep-dive comparing embedding-similarity, hierarchical-clustering, and LLM-based semantic chunking methods