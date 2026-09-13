---
tags:
  - gen_ai
  - gen_ai/rag
created: 2024-11-28T19:22
modified: 2026-03-02T10:39
published:
sources:
  - "[RAPTOR: RECURSIVE ABSTRACTIVE PROCESSING FOR TREE-ORGANIZED RETRIEVAL](https://arxiv.org/pdf/2401.18059)"
topics:
  - RAPTOR
  - Hierarchical Retrieval
  - Recursive Summarization
  - Gaussian Mixture Models
authors:
ai-assisted:
hidden:
public: true
---
# Raptor
- [RAPTOR PAPER](https://arxiv.org/pdf/2401.18059):
> We introduce the novel approach of recursively embedding, clustering, and summarizing chunks of text, constructing a tree with differing levels of summarization from the bottom up. At inference time, our RAPTOR model retrieves from this tree, integrating information across lengthy documents at different levels of abstraction. Controlled experiments show that retrieval with recursive summaries offers significant improvements over traditional retrieval-augmented LMs on several tasks.
## Clustering Algorithm
- Soft clustering through Gaussian Mixture Models (GMMs).
	- Soft clustering is essential because individual text segments often contain information relevant to various topics, thereby warranting their inclusion in multiple summaries.
	- To determine the optimal number of clusters, we employ the Bayesian Information Criterion (BIC) for model selection.
	- the Gaussian assumption in GMMs may not perfectly align with the nature of text data, which often exhibits a sparse and skewed distribution, our empirical observations suggest that it offers an effective model for our purpose.
	- Should a local cluster’s combined context ever exceed the summarization model’s token threshold, our algorithm recursively applies clustering within the cluster, ensuring that the context remains within the token threshold.
## Querying
The two querying mechanisms employed by RAPTOR: tree traversal and collapsed tree.
### [[Tree traversal]]
Selects the top-k most relevant root nodes based on their cosine similarity to the query embedding. The children of these selected nodes are considered at the next layer and the top-k nodes are selected from this pool again based on their cosine similarity to the query vector. This process is repeated until we reach the leaf nodes.
### [[Collapsed tree]]
Instead of going layer-by-layer, this method flattens the multi-layered tree into a single layer, essentially bringing all the nodes onto the same level for comparison. Therefore, just doing similarity search on the all nodes basically.

**This method works better based on the paper findings.**
<img src="https://archive.ph/Zgb13/b1f0822f0495dfe243264448768280bc36009961.webp"/>