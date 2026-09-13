---
tags:
  - gen_ai
  - gen_ai/rag
created:
modified: 2026-08-06T08:58
published:
sources:
  - "[Pinecone Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/)"
  -  [Searching for Best Practices in RAG](https://aclanthology.org/2024.emnlp-main.981.pdf)
  - "[RAG for LLMs: A Survey](https://arxiv.org/pdf/2312.10997)"
topics:
  - Chunking
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Chunking
- In the context of building LLM-related applications, **chunking** is the process of breaking down large pieces of text into smaller segments. It’s an essential technique that helps optimize the relevance of the content we get back from a vector database once we use the LLM to embed content.

- There are multiple aspects to the chunking processes such as:
	- [[Chunk Size]]
	- [[Chunking Strategies]]
	- Metadata Addition
		- Enhancing chunk blocks with metadata like titles, keywords, and hypothetical questions can improve retrieval, provide more ways to post-process retrieved texts, and help LLMs better understand retrieved information.