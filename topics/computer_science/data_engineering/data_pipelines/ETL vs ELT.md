---
tags:
  - cs
  - cs/data_eng
created: 2026-03-14T00:00
modified: 2026-07-26T13:27
published:
sources:
  - "[ETL vs ELT: What's the Difference? – Databricks](https://www.databricks.com/glossary/etl-vs-elt)"
topics:
  - ETL
  - ELT
  - Data Transformation
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# ETL vs ELT
- Two dominant patterns for moving data from source systems into an analytical destination.

## ETL — Extract, Transform, Load
Data is transformed **before** it reaches the destination.
1. **Extract** — pull raw data from sources (DBs, APIs, files)
2. **Transform** — clean, join, aggregate in an intermediate engine (e.g. Spark job, custom script)
3. **Load** — write the clean, structured result to the warehouse/data lake

- Originated when storage was expensive and warehouses were rigid
- Transformation logic lives **outside** the warehouse
- Tools: Apache Spark, Talend, Informatica, custom Python scripts
## ELT — Extract, Load, Transform
Data is loaded raw first; transformation happens **inside** the warehouse.
1. **Extract** — pull raw data from sources
2. **Load** — dump raw data into the warehouse/lake (cheap columnar storage)
3. **Transform** — use SQL (e.g. [dbt](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fdata_engineering%2Fdata_pipelines%2Fdbt)) to model data directly in the warehouse

- Made practical by cheap cloud storage and powerful MPP warehouses (Snowflake, BigQuery, Redshift, Databricks)
- Transformation logic lives **inside** the warehouse as SQL models
- Enables reproducibility, version control, and easy re-runs
## Comparison

| Dimension           | ETL                            | ELT                                                                                                                           |
| ------------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| Transform location  | External engine                | Inside the warehouse                                                                                                          |
| Raw data preserved? | Often not                      | Yes (always in source layer)                                                                                                  |
| Scalability         | Depends on transform engine    | Inherits warehouse scale                                                                                                      |
| Tooling             | Spark, custom scripts          | [dbt](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fdata_engineering%2Fdata_pipelines%2Fdbt), Dataform |
| Latency             | Higher (transform before load) | Lower initial load                                                                                                            |
| Re-processing       | Harder                         | Easy (re-run SQL)                                                                                                             |

## When to Use Which
- **ETL** — when raw data must not touch the warehouse (compliance), when transformation is computationally heavy (ML feature engineering), or when the destination is not SQL-capable
- **ELT** — most modern cloud analytics workloads; preferred pattern with [dbt](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fdata_engineering%2Fdata_pipelines%2Fdbt) and cloud warehouses
