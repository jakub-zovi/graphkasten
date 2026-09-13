---
tags:
  - cs
  - cs/databases
created: 2024-11-04T09:15
modified: 2025-08-09T11:27
published:
sources:
topics:
  - Hash-based Indexes
  - LSH
  - ANN Indexes
authors:
ai-assisted:
hidden:
public: true
---
# Hash-based
[Learned Indexing in Vector Database Management Systems:](https://theses.cz/id/j9zbws/?lang=en)
> Hash-based methods transform the high dimensional vectors into the low dimensional hash signature. They do this by hashing the vectors multiple times. The main assumption of this type of methods is that similar data points will end up in the same hash buckets. This assumption is i n contrast to traditional hashing, where the main premise is to avoid bucket collisions. The need for bucket collisions heavily affects the choice of hash function. 