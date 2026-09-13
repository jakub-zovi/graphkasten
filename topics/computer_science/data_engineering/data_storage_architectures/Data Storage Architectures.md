---
tags:
  - cs
  - cs/data_eng
created: 2024-10-06T10:30
modified: 2026-07-26T13:24
published:
sources:
topics:
  - Data Storage Architectures
  - Delta Lake
  - Apache Iceberg
  - Table Formats
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Data Storage Architectures
Data Storage and Analytics Architectures encompass the systems and frameworks used to store, manage, and analyze large volumes of structured, semi-structured, and unstructured data.
## Topics
- [[Data Warehouse]]
- [[Data Lake]]
- [[Delta Lake]]
- [[Data Lakehouse]]
- [[Apache Iceberg]]
	- Open table format for huge analytic datasets; multi-engine, cloud-agnostic alternative to Delta Lake

## Table Format Comparison
| Aspect | Delta Lake | Apache Iceberg |
|---|---|---|
| Origin | Databricks (2019) | Netflix → Apache (2020) |
| Engine support | Spark-first; growing connector ecosystem | Spark, Flink, Trino, Presto, Hive, Impala, Dremio, … |
| Hidden partitioning | No — partition columns explicit in queries | Yes — transforms at write; queries engine-agnostic |
| Partition evolution | Requires full rewrite | Change spec without rewriting old data |
| Catalog flexibility | Tight Databricks/Unity Catalog coupling | Any catalog (REST, Glue, Nessie, HMS) |
| Metadata format | JSON transaction log (`_delta_log/`) | JSON (table metadata) + Avro (manifests) |
| Ecosystem traction | Dominant in Databricks/Azure environments | Strong in AWS/GCP, cloud-agnostic ecosystems |