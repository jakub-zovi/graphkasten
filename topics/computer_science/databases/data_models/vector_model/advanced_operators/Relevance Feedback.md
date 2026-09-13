---
tags:
  - cs
  - cs/databases
created: 2026-03-02T00:00
modified: 2026-07-26T13:43
published:
sources:
topics:
  - Relevance Feedback
  - Vector Search
  - Information Retrieval
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Relevance Feedback
- [Relevance feedback - Wikipedia](https://en.wikipedia.org/wiki/Relevance_feedback)
	- Relevance feedback is an iterative process that refines search results based on user interactions. After a system returns initial results, the user marks specific documents as relevant or irrelevant. The system then updates the query and searches again to improve precision and recall.
	- Three types of feedback: explicit feedback, implicit feedback, and blind or "pseudo" feedback.
## Resources
- [[Relevance Feedback in Qdrant]] ([Link](https://qdrant.tech/articles/relevance-feedback/))
	- 2026-02-19
- [[Relevance Feedback in Informational Retrieval]] ([Link](https://qdrant.tech/articles/search-feedback-loop/))
	- 2025-03-26
## Discussions With AI
- [[Claude Discussion - Relevance feedback & Wormhole Vectors]]
	- Walk-through of how the Qdrant relevance feedback formula replaces cosine similarity on the second pass