---
tags:
  - cs
  - cs/data_eng
created: 2024-10-08T14:49
modified: 2025-08-19T07:22
published:
sources:
  - "[DBX Medallion Architecture](https://www.databricks.com/glossary/medallion-architecture)"
topics:
  - Medallion Architecture
  - Data Pipelines
  - Lakehouse
  - Bronze Silver Gold
authors:
ai-assisted:
hidden:
public: true
---
# Medallion Architecture
A **medallion architecture** is a data design pattern used to logically organize data in a [lakehouse](https://www.databricks.com/glossary/data-lakehouse), with the goal of incrementally and progressively improving the structure and quality of data as it flows through each layer of the architecture (from Bronze ⇒ Silver ⇒ Gold layer tables). Medallion architectures are sometimes also referred to as "multi-hop" architectures.
## Bronze layer (raw data)
The **[[Bronze layer]]** is where we land all the data from external source systems. The table structures in this layer correspond to the source system table structures =="as-is,"== along with any additional metadata columns that capture the load date/time, process ID, etc.
## Silver layer (cleansed and conformed data)
In the **[[Silver layer]]** of the lakehouse, the data from the Bronze layer is matched, merged, conformed and cleansed ("just-enough") so that the Silver layer can provide an =="Enterprise view"== of all its key business entities, concepts and transactions.
## Gold layer (curated business-level tables)
Data in the **[[Gold layer]]** of the lakehouse is typically organized in consumption-ready =="project-specific"== databases. The Gold layer is for reporting and uses more de-normalized and read-optimized data models with fewer joins. The final layer of data transformations and data quality rules are applied here.

<img src="https://www.databricks.com/sites/default/files/inline-images/building-data-pipelines-with-delta-lake-120823.png?v=1702318922">

