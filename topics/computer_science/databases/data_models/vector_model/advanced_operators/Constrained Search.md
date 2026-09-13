---
tags:
  - cs
  - cs/databases
created: 2024-11-04T09:18
modified: 2025-08-09T11:27
published:
sources:
topics:
  - Constrained Search
  - Filtering
  - Vector Search
authors:
ai-assisted:
hidden:
public: true
---
# Constrained Search (Filtering)
This type of search extends classical kANN search by applying a constraint that the resulting set of nearest neighbours must satisfy. This can greatly improve the quality of the result since we are only searching in the area of interest within our dataset [(LI in VDBMS)](https://is.muni.cz/th/hsfz1/).

💡It is ideal to employ this type of search when you can estimate the topic or category that the user is asking about. Also, you can prompt the user for some information about him, which again gives the opportunity to narrow the search space with the use of filtering.
## Resources
- [[Vector Search in the Real World - How to Filter Efficiently Without Killing Recall]] ([Link](https://milvus.io/blog/how-to-filter-efficiently-without-killing-recall.md))
	- 2025-05-12
	- Milvus blog on filtering inside graph indexes — Alpha Strategy, ACORN, dynamic neighbor selection, and Milvus/Cardinal's adaptive include-all/exclude-all switching to preserve recall under selective filters