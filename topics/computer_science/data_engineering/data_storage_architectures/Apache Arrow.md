---
tags:
  - cs
  - cs/data_eng
created: 2025-04-15T16:44
modified: 2026-07-19T15:19
published:
sources:
  - "[Apache Arrow](https://www.heavy.ai/technical-glossary/apache-arrow),  [Difference between Apache parquet and arrow](https://stackoverflow.com/questions/56472727/difference-between-apache-parquet-and-arrow), [Parquet vs. Arrow](https://medium.com/@diehardankush/comparing-data-storage-parquet-vs-arrow-aa2231e51c8a)"
topics:
  - Apache Arrow
  - Columnar Memory Format
  - In-Memory Processing
authors:
ai-assisted:
hidden:
public: true
---
# Apache Arrow
- [Apache Arrow](https://www.heavy.ai/technical-glossary/apache-arrow):
> Apache Arrow is a platform that analyzes the memory in a server’s random access memory (RAM). It works in any computer language and defines a columnar memory format standard. The columnar layout allows for faster processing of data than rows. Apache Arrow performance also provides computational libraries and saves the central processing unit (CPU) from having to copy data from one memory area to another.
## Data Storage (Arrow vs Parquet)
- [Parquet vs. Arrow](https://medium.com/@diehardankush/comparing-data-storage-parquet-vs-arrow-aa2231e51c8a):
> Parquet is a disk-based storage format, while Arrow is an in-memory format. Parquet is optimized for disk I/O and can achieve high compression ratios with columnar data. This is an advantage when working with large data sets where disk space might be a concern.
> 
> In contrast, Arrow is designed for high-speed in-memory data processing. It provides a standardized language-agnostic format for flat and hierarchical data, which is optimized for modern CPUs.