---
tags:
  - cs
  - cs/databases
created: 2024-10-29T20:43
modified: 2025-08-09T11:27
published:
sources:
  - "[Learned Indexing in Vector Database Management Systems](https://is.muni.cz/th/hsfz1/Learned_Indexing_in_Vector_Database_Management_Systems_Archive.pdf)"
topics:
  - k-ANN Query
  - ANN Search
  - Approximation Error
authors:
ai-assisted:
hidden:
public: true
---
# k-ANN query
$kANN(q)=\{|R| = k \land \forall x \in R, y \in X - R: d(q, x) \leq (1+\epsilon) d(q, y)\}$
where $\epsilon$ represents the approximation error ($\epsilon \geq 0$) and $k$ specifies the size of the returned set.
When $\epsilon=0$ and the 1 , an NN search is performed.
