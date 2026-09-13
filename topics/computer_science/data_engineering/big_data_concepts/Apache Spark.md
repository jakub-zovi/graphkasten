---
tags:
  - cs
  - cs/data_eng
created: 2024-10-11T17:38
modified: 2026-09-08T09:54
published:
sources:
  -  [IBM](https://www.ibm.com/think/insights/hadoop-vs-spark)
topics:
  - Apache Spark
  - RDD
  - Distributed Computing
  - In-Memory Processing
authors:
  - Jakub
ai-assisted:
hidden:
public: true
banner: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQr9kkAksedf-kECODK9Cmae0W1si3R1KQpKCo0xopxNQ&s=10
content-start: 511
banner-height: 550
banner-max-width: 1450
---
# Apache Spark
- [IBM](https://www.ibm.com/think/insights/hadoop-vs-spark)
> Apache Spark — which is also open source — is a data processing engine for big data sets. Like [[Hadoop]], Spark splits up large tasks across different nodes. **However, it tends to perform faster than Hadoop and it [[Uses RAM]] to cache and process data instead of a file system.** This enables Spark to handle use cases that Hadoop cannot.
- Spark solves the limitation of the [[Hadoop]], it also uses [[Map-Reduce]] paradigm. It provides a more expressive API than Hadoop's MapReduce and supports a wider range of operations beyond just Map and Reduce, including transformations like `map`, `flatMap`, `filter`, `reduceByKey`, `join`, and more. Unlike Hadoop, **Spark** performs in-memory computations.
- Spark’s **core abstraction** is the **[[RDD]] (Resilient Distributed Dataset)**.
	- An RDD is a **distributed collection of objects** that Spark can process in parallel across a cluster
	- By default, RDDs are **transient**. They’re recomputed whenever needed, unless you explicitly ask Spark to _cache_ or _persist_ them.
	- If you `persist()` an RDD, Spark can keep it in memory, spill it to local disk, or even replicate it — depending on the storage level you choose.
- Apache **Spark itself does not come with a built-in persistent storage layer**. It’s a distributed compute engine — it needs some storage system to read input data from and optionally write output to. Example of storage systems:
	- HDFS
	- Local file systems
	- Cloud storage
## Concepts
- [[Spark Core Concepts]]
- [[PySpark Reference]]
- [[Spark Data Structures]]
- [[Optimize Spark]]