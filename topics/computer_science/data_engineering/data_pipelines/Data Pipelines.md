---
tags:
  - cs
  - cs/data_eng
created: 2026-03-14T00:00
modified: 2026-07-26T13:24
published:
sources:
  - "[What is a data pipeline?](https://www.ibm.com/think/topics/data-pipeline)"
topics:
  - Data Pipelines
  - Workflow Orchestration
  - Data Transformation
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Data Pipelines
- [What is a data pipeline?](https://www.ibm.com/think/topics/data-pipeline)
> A data pipeline is a system that ingests raw data from multiple data sources, transforms it and then loads it into a data store such as a [data lake](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fdata_engineering%2Fdata_storage_architectures%2FData%20Lake) or [data warehouse](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fdata_engineering%2Fdata_storage_architectures%2FData%20Warehouse) for analysis and operational use.
- Pipelines handle ingestion, transformation, validation, and loading
## Topics
- [[Airflow]]
	- DAG-based workflow orchestrator; schedules and monitors pipeline steps
- [[Medallion Architecture]]
	- Layered data quality pattern: Bronze → Silver → Gold
- [[ETL vs ELT]]
	- Comparison of the two dominant pipeline patterns and when to use each
