---
tags:
  - cs
  - cs/data_eng
created: 2024-10-06T11:00
modified: 2025-08-08T19:04
published:
sources:
topics:
  - Delta Lake
  - ACID Transactions
  - Lakehouse
  - Parquet
authors:
ai-assisted:
hidden:
public: true
---
# Delta Lake
**[DBX definition:](https://docs.databricks.com/en/delta/index.html)**
> Delta Lake is the optimized storage layer that provides the foundation for tables in a lakehouse on Databricks. Delta Lake is [open source software](https://delta.io/) that extends [[Parquet]] data files with a file-based transaction log for [ACID transactions](https://docs.databricks.com/en/lakehouse/acid.html) and scalable metadata handling.

**Features:**
- ACID transaction guarantees
- Scalable data and metadata handling
- Audit history and time travel
- Schema enforcement and schema evolution
- Support for deletes, updates, and merges
- Unified streaming and batch data processing
Delta lake uses [[Delta Table]]s to organize data into tabular format.
## Managing files and indexing data
- [[Liquid Clustering]]
