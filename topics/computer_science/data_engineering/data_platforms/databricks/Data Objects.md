---
tags:
  - cs
  - cs/data_eng
created: 2024-10-16T13:11
modified: 2025-08-08T19:04
published:
sources:
topics:
  - Databricks
  - Unity Catalog
  - Tables and Volumes
  - Data Governance
authors:
ai-assisted:
hidden:
public: true
---
# Data Objects
[DBX:](https://docs.databricks.com/en/database-objects/index.html)
> Databricks uses two primary securable objects to store and access data.
> - [[Tables]] govern access to tabular data.
> - [[Volumes]] govern access to non-tabular data.
> 
> Database objects are entities that help you organize, access, and govern data. Databricks uses a three-tier hierarchy to organize database objects:
> 
> 1. **Catalog**: The top level container, contains schemas.
> 2. **Schema** or database: Contains data objects.
> 3. Data objects that can be contained in a schema:
>     - **Volume**: a logical volume of non-tabular data in cloud object storage.
>     - **Table**: a collection of data organized by rows and columns.
>     - **View**: a saved query against one or more tables
>     - **Function**: saved logic that returns a scalar value or set of rows.
>     - **Model**: a machine learning model packaged with MLflow.
>     - 
> Catalogs are registered in a metastore that is managed at the account level. Only admins interact directly with the metastore.

<div>
<img src="https://docs.databricks.com/en/_images/object-model.png"></div>


[[Data Governance]] is handled by unity catalog in the DBX.