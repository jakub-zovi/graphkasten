---
tags:
  - cs
  - cs/data_eng
created: 2026-03-18T10:00
modified: 2026-07-26T13:19
published:
sources:
  - "[Apache Iceberg Docs](https://iceberg.apache.org/docs/latest/)"
  - "[Apache Iceberg: An Architectural Look Under the Covers](https://www.dremio.com/resources/guides/apache-iceberg-an-architectural-look-under-the-covers/)"
  - "[Delta Lake vs Apache Iceberg](https://www.databricks.com/blog/delta-lake-vs-apache-iceberg)"
topics:
  - Table Format
  - Open Table Format
  - Data Lakehouse
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Apache Iceberg
- Apache Iceberg is an open table format for huge analytic datasets. Originally developed at Netflix to solve large-scale data correctness and performance problems, it became a top-level Apache project in 2020.
> Iceberg is a high-performance format for huge analytic tables. Iceberg brings the reliability and simplicity of SQL tables to big data, while making it possible for engines like Spark, Trino, Flink, Presto, Hive and Impala to safely work with the same tables, at the same time. ([Apache Iceberg Docs](https://iceberg.apache.org/docs/latest/))

## Key Features
- **ACID transactions** — serializable isolation with optimistic concurrency
- **Schema evolution** — add, drop, rename, reorder columns without rewrites; type promotion supported
- **Hidden partitioning** — partition transforms applied automatically; queries don't require partition filter knowledge
- **Time travel** — query any historical snapshot by timestamp or snapshot ID
- **Row-level operations** — copy-on-write (CoW) and merge-on-read (MoR) strategies for deletes/updates/upserts
- **Multi-engine support** — Spark, Flink, Trino, Presto, Hive, Impala, Dremio, StarRocks, and more
- **Partition evolution** — change partitioning strategy without rewriting existing data

## Metadata Structure
Iceberg uses a layered metadata hierarchy to track all data files and changes:

```
Catalog
└── Table Metadata (JSON)
    └── Snapshot
        └── Manifest List (Avro)
            └── Manifest Files (Avro)
                └── Data Files (Parquet / ORC / Avro)
```

- **Table Metadata file (JSON)** — current snapshot pointer, schema, partition spec, sort order
- **Snapshot** — immutable point-in-time state of the table; each write creates a new snapshot
- **Manifest list** — lists all manifest files for a snapshot with partition-level stats (enables partition pruning)
- **Manifest file** — lists data files with column-level stats (enables column/row group pruning)
- **Data files** — actual columnar data in [[Parquet]], ORC, or Avro

This design means metadata operations (schema changes, time travel) are just pointer swaps — no data rewriting needed.

## vs [[Delta Lake]]

| Aspect | Apache Iceberg | Delta Lake |
|---|---|---|
| Origin | Netflix → Apache (2020) | Databricks (2019), open-sourced |
| Engine support | Spark, Flink, Trino, Presto, Hive, Impala, Dremio, … | Spark-first; growing (Flink, Trino connectors exist) |
| Hidden partitioning | Yes — transforms applied at write; queries engine-agnostic | No — partition columns must be explicit in queries |
| Partition evolution | Yes — change spec without rewriting old data | No — requires full rewrite to repartition |
| Catalog flexibility | Any catalog (REST, Glue, Nessie, HMS) | Tightly coupled to Databricks Unity Catalog or HMS |
| Metadata format | JSON (table metadata) + Avro (manifests) | JSON transaction log (`_delta_log/`) |
| Row-level DML strategy | CoW or MoR (configurable per table) | CoW default; MoR (deletion vectors) added later |
| Ecosystem traction | Cloud-agnostic; strong in AWS/GCP ecosystems | Dominant in Databricks/Azure environments |

## vs [[Delta Table]]
[[Delta Table]] is a Databricks-specific abstraction **on top of** [[Delta Lake]] — it is the managed/unmanaged table object registered in the Databricks catalog. Iceberg has no equivalent separation: an Iceberg table is a first-class object defined by its metadata files, not by a platform-specific catalog entry. This makes Iceberg inherently more portable across clouds and engines.
