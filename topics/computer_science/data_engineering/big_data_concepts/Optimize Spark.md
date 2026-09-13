---
tags:
  - cs
  - cs/data_eng
created: 2025-01-15T15:58
modified: 2025-08-08T19:04
published:
sources:
topics:
  - Apache Spark
  - Spark Optimization
  - Partitioning
  - Catalyst
authors:
ai-assisted:
hidden:
public: true
--- 
# Optimize Spark
- Use `cache()` and `persist()` strategically for reusing data.
- Leverage partitioning and bucketing for data shuffling efficiency.
- Optimize the number of partitions to balance parallelism and overhead.
- Avoid wide transformations when possible to minimize shuffle operations.
- Use Broadcast variables for smaller datasets shared across nodes.
- Enable Tungsten and Catalyst optimizations for SQL queries.