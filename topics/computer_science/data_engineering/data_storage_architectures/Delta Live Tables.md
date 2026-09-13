---
tags:
  - cs
  - cs/data_eng
created: 2024-10-08T22:07
modified: 2026-07-19T15:22
published:
sources:
topics:
  - Delta Live Tables
  - Databricks
  - Data Pipelines
  - Declarative ETL
authors:
ai-assisted:
hidden:
public: true
---
# Delta Live Tables
- **Delta Live Tables** (DLT) is a more recent feature introduced by Databricks to automate and simplify the **management of data pipelines**. While Delta Live Tables use the same Delta Lake format for storage, they add more functionality and ease-of-use for data engineering workflows. The key differences include:

#### Features of Delta Live Tables:
- **Declarative ETL pipelines**: DLT allows you to define data transformation pipelines declaratively using SQL or Python. You focus on "what" transformations need to happen rather than "how" to implement them.
- **Automatic management**: Delta Live Tables automatically manages the complexity of pipeline execution, such as handling dependencies, optimizing execution, and error handling.
- **Continuous or scheduled pipeline execution**: DLT can run pipelines continuously (streaming) or on a scheduled batch mode, making it easier to manage both real-time and batch processing.
- **Data quality management**: DLT comes with built-in features like **expectations** for data quality. These allow you to define rules for data validation, and the pipeline can automatically handle invalid data (e.g., logging, quarantining, or correcting).
- **Versioning and monitoring**: DLT provides comprehensive logging and versioning, along with monitoring capabilities. The Databricks workspace offers a UI that lets you track pipeline runs, check data lineage, and monitor health.

#### Comparison:
- **Delta Table**: You create and manage a table, using Delta Lake's features for data storage and querying, but you are responsible for building, orchestrating, and maintaining the pipeline that feeds this table.
- **Delta Live Table**: DLT abstracts much of the pipeline management complexity and introduces advanced features like monitoring, automatic error handling, and data quality expectations. It also supports both batch and streaming data processing, with built-in optimization for pipeline execution.