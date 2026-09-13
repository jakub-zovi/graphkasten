---
tags:
  - gen_ai
  - gen_ai/models
created: 2025-05-06T17:13
modified: 2026-08-01T18:47
published:
sources:
  - "[What is the difference between sparse and dense retrieval?](https://milvus.io/ai-quick-reference/what-is-the-difference-between-sparse-and-dense-retrieval)"
topics:
  - Sparse Retrieval
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Sparse Retrieval
- [What is the difference between sparse and dense retrieval?](https://milvus.io/ai-quick-reference/what-is-the-difference-between-sparse-and-dense-retrieval)
> Sparse retrieval methods, like TF-IDF or BM25, represent text as high-dimensional vectors where most dimensions are zero, encoding the presence or absence of specific words.
- Their main goal is to do [[Keyword Search]] or something between keyword and semantic search i.e. sparse retrieval
## Methods
Source: ChatGPT[^1]
- [[Traditional Sparse Retrieval]]
- [[Learned Sparse Retrieval]]
## Resources
- [[Keyword search is all you need]]: Achieving RAG-Level Performance without vector databases using agentic tool use
	- [Paper](https://arxiv.org/pdf/2602.23368) by AWS
## Comparison
ChatGPT[^1] (**Note that BGE-M3 is not in the table**):

| Feature                      | **BM25**              | **BM25 + WordPiece**           | **SPLADE**                | **BM42**                      |
| ---------------------------- | --------------------- | ------------------------------ | ------------------------- | ----------------------------- |
| Tokenization                 | Words                 | Subwords                       | Subwords                  | Flexible                      |
| Semantic Matching            | ❌ No                  | ⚠️ Partial (via overlap)       | ✅ Yes                     | ✅ Yes                         |
| Requires Training            | ❌ No                  | ❌ No                           | ✅ Yes                     | ✅ Yes                         |
| Document Encoding Speed      | ⚡ Fast                | ⚡ Fast                         | 🐢 Slow                   | ⚡ Fast                        |
| Query Encoding Speed         | ⚡ Fast                | ⚡ Fast                         | 🐢 Slow                   | ⚡ Fast                        |
| Interpretable                | ✅ Yes                 | ⚠️ Somewhat                    | ✅ Yes                     | ✅ Yes                         |
| Matches Without Shared Terms | ❌ No                  | ❌ No                           | ✅ Yes                     | ✅ Yes                         |
| Best Use Case                | Simple keyword search | Morphologically rich languages | Semantically fuzzy search | Fast semantic + hybrid search |

[^1]: Prompts: "Can you explain BM25 vs BM25 + Word Piece Tokenizer vs SPLADE", "What about BM42 from Qdrant?", "Can you again in a structured fashion described each of these methods: BM25, BM25 + WordPiece tokenizers, SPLADE, BM42"