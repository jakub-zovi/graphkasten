---
tags:
  - cs
  - cs/databases
created: 2024-10-29T11:21
modified: 2025-08-09T11:27
published:
sources:
topics:
  - Similarity Search
  - Nearest Neighbor Search
  - ANN Search
  - Vector Search
authors:
ai-assisted:
hidden:
public: true
---
# Similarity Searching
In order to search unstructured data, we perform a similarity search, more commonly called a **nearest neighbour (NN) search**. This search tries to find the nearest object to the query based on the defined distance (similarity) function.

Finding the nearest object can be done exhaustively by computing the distance between the query and every object in the database, but this is not scalable to large datasets. Ideally, we would want to use some indexing algorithm, but currently, no algorithm exists for NN search that outperforms brute force search.

Therefore, in practice, we use the **approximate nearest neighbour (ANN) search**. This type of search does not guarantee finding the best possible answer i.e. the most similar object. For ANN search, a lot of [[ANN indexes]] algorithms exist that we can use in practice. Also, in practice, we use k-ANN search, meaning we retrieve k nearest approximate neighbours.

- [[Metric space]] definition
- [[k-ANN query]] definition

💡**Use brute force search when you are dealing with a small dataset! The rule of thumb is to use brute force when you have less than 20,000 objects in the database ([google-research ScaNN recommendation](https://github.com/google-research/google-research/blob/master/scann/docs/algorithms.md#rules-of-thumb)).**