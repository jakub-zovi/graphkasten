---
tags:
  - cs
  - cs/data_eng
created: 2025-01-15T15:35
modified: 2026-08-02T09:31
published:
sources:
topics:
  - Apache Spark
  - RDD
  - DAG
  - Spark Architecture
  - Lazy Evaluation
authors:
ai-assisted:
hidden:
public: true
---
Footnote Sources: ChatGPT[^1]
# Spark Core Concepts
# Apache Spark: Theoretical Overview

Apache Spark is a powerful open-source distributed computing system designed for large-scale data processing. It provides an easy-to-use interface for batch, streaming, and interactive data analytics. Below is a theoretical description of Spark, covering its key concepts and features, often discussed in interviews.

---

## Core Concepts

### 1. **Resilient Distributed Dataset (RDD)**
- RDD is the fundamental data structure in Spark.
- It is an immutable distributed collection of objects that can be processed in parallel.
- RDDs support two types of operations:
  - **Transformations:** Create a new RDD from an existing one (e.g., `map`, `filter`).
  - **Actions:** Trigger computation and return results (e.g., `count`, `collect`).

### 2. **Directed Acyclic Graph (DAG)**
- Spark uses a DAG to represent the sequence of operations to be performed on data.
- DAGs optimize execution by reducing redundant computations and improving resource utilization.

### 3. **Lazy Evaluation**
- Transformations on RDDs are not executed immediately but are recorded as metadata until an action is invoked.
- This approach allows Spark to optimize the execution plan.

---

## Features

### 1. **In-Memory Processing**
- Spark processes data in memory, which significantly enhances performance compared to traditional disk-based systems like Hadoop MapReduce.

### 2. **Fault Tolerance**
- Spark automatically recovers lost RDD partitions using lineage information.
- It re-computes lost partitions from the original RDDs.

### 3. **High-Level APIs**
- Spark provides high-level APIs for Java, Scala, Python, and R.
- It includes libraries for SQL (Spark SQL), machine learning (MLlib), graph processing (GraphX), and streaming (Spark Streaming).

### 4. **Unified Engine**
- Spark supports batch, interactive, and streaming workloads on a single platform, reducing the need for multiple systems.

---

## Spark Components

### 1. **Spark Core**
- The foundational engine for Spark, managing memory, scheduling, fault tolerance, and distributed tasks.

### 2. **Spark SQL**
- A module for structured data processing.
- Supports SQL queries, DataFrames, and integration with external data sources (e.g., Hive, JDBC).

### 3. **Spark Streaming**
- Enables real-time processing of streaming data.
- Data is divided into mini-batches and processed incrementally.

### 4. **MLlib**
- A scalable machine learning library with algorithms for classification, regression, clustering, and collaborative filtering.

### 5. **GraphX**
- A library for graph processing and graph-parallel computation.

---

## Cluster Architecture

### 1. **Driver**
- The driver program initiates the Spark application.
- It converts user code into a DAG and schedules tasks.

### 2. **Executor**
- Executors run on worker nodes to execute tasks and store data in memory or disk.
- They communicate with the driver for task status updates.

### 3. **Cluster Manager**
- Manages resources in the cluster.
- Examples include YARN, Mesos, or Spark's standalone cluster manager.

---

## Key Interview Topics

### 1. **How Spark Achieves Fault Tolerance**
- RDD lineage tracks operations to re-compute lost data.
- Data persistence options (`MEMORY_AND_DISK`, etc.) allow flexible fault tolerance strategies.

### 2. **Difference Between Transformations and Actions**
- Transformations are lazy and create a new RDD; actions trigger execution and return results.
- Examples:
  - Transformation: `map`, `filter`
  - Action: `count`, `collect`

### 3. **Advantages Over Hadoop MapReduce**
- In-memory processing
- Unified API for batch and streaming data
- Richer APIs for data transformation

### 4. **Optimizations in Spark**
- Catalyst optimizer for Spark SQL
- Tungsten execution engine for efficient memory and CPU usage
- DAG scheduling and task pipelining

### 5. **What Is Broadcast and Accumulator?**
- **Broadcast Variables:** Share large read-only data across all nodes efficiently.
- **Accumulators:** Aggregate values from worker nodes back to the driver (e.g., for counting errors).

### 6. **Difference Between DataFrame and Dataset**
- **DataFrame:** Distributed collection of data organized into named columns, similar to a table in a database.
- **Dataset:** Strongly typed, object-oriented API for structured data (available in Scala and Java).

[^1]: Prompt: Great, now can you give a more theoretical description of the Spark. Try to cover aspects that are often asked at interview.
[^2]: Test