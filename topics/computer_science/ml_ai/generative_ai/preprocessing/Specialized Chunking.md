---
tags:
  - gen_ai
  - gen_ai/rag
created: 2025-02-07T16:38
modified: 2026-08-02T10:12
published:
sources:
  - "[Pinecone Chunking Strategies](https://www.pinecone.io/learn/chunking-strategies/)"
topics:
  - Chunking
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Specialized Chunking
Markdown and LaTeX are two examples of structured and formatted content you might run into.
### Markdown
```python
from langchain.text_splitter import MarkdownTextSplitter
markdown_text = "..."

markdown_splitter = MarkdownTextSplitter(chunk_size=100, chunk_overlap=0)
docs = markdown_splitter.create_documents([markdown_text])
```
### Latex
```python
from langchain.text_splitter import LatexTextSplitter
latex_text = "..."
latex_splitter = LatexTextSplitter(chunk_size=100, chunk_overlap=0)
docs = latex_splitter.create_documents([latex_text])
```

