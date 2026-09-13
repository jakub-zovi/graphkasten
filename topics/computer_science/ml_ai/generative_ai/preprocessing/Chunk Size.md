---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-08T11:56
modified: 2026-08-02T10:19
published:
sources:
  - "[Searching for Best Practices in RAG](https://aclanthology.org/2024.emnlp-main.981.pdf)"
topics:
  - Chunking
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Chunk Size
- [Searching for Best Practices in RAG](https://aclanthology.org/2024.emnlp-main.981.pdf):
> Chunk size significantly impacts performance. Larger chunks provide more context, enhancing comprehension but increasing process time. Smaller chunks improve retrieval recall and reduce time but may lack sufficient context.


Generally, the chunk strategy and the size have to be fine tuned for specific situation, but the paper [Searching for Best Practices in RAG](https://aclanthology.org/2024.emnlp-main.981.pdf) provides at least some guide what should be good starting chunking size of **256** with overlap of 20 tokens:

| Chunk Size | Average Faithfulness | Average Relevancy |
| ---------- | -------------------- | ----------------- |
| 2048       | 80.37                | 91.11             |
| 1024       | 94.26                | 95.56             |
| 512        | **97.59**            | 97.41             |
| 256        | 97.22                | **97.78**         |
| 128        | 95.74                | 97.22             |
Table 3: Comparison of different chunk sizes for **lyft_2021** dataset.
