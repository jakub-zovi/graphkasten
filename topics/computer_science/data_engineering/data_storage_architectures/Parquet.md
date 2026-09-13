---
tags:
  - cs
  - cs/data_eng
created: 2024-10-08T22:09
modified: 2025-11-08T18:12
published:
sources:
  - "[What is Parquet?](https://www.databricks.com/glossary/what-is-parquet)"
topics:
  - Parquet
  - Columnar Storage
  - File Formats
authors:
ai-assisted:
hidden:
public: true
---
# Parquet
Apache Parquet is an open source, column-oriented data file format designed for efficient data storage and retrieval. It provides efficient data compression and encoding schemes with enhanced performance to handle complex data in bulk. Apache Parquet is designed to be a common interchange format for both batch and interactive workloads. It is similar to other columnar-storage file formats available in [Hadoop](https://www.databricks.com/glossary/hadoop), namely [[RCFile]] and [[ORC]].
As mentioned above, Apache Parquet is storage format unlike [[Apache Arrow]] which is an in-memory data processing framework.
## Characteristics of Parquet
- **Free and open source file format.**
- **Language agnostic.**
- **[[Column-based format]]** - files are organized by column, rather than by row, which saves storage space and speeds up analytics queries.
- **Used for analytics (OLAP) use cases**, typically in conjunction with traditional OLTP databases.
- **Highly efficient** data compression and decompression.
- **Supports complex data types** and advanced nested data structures.
## Benefits of Parquet
- **Good for storing big data of any kind** (structured data tables, images, videos, documents).
- **Saves on cloud storage space** by using highly efficient column-wise compression, and flexible encoding schemes for columns with different data types.
- **Increased data throughput and performance** using techniques like data skipping, whereby queries that fetch specific column values need not read the entire row of data.