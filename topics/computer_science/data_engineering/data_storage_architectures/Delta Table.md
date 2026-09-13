---
tags:
  - cs
  - cs/data_eng
created: 2024-10-08T21:37
modified: 2025-08-08T19:04
published:
sources:
topics:
  - Delta Table
  - Delta Lake
  - Databricks
  - Managed vs External Tables
authors:
ai-assisted:
hidden:
public: true
---
# Delta Table
A **Delta Table** is a regular table in Databricks that uses the **Delta Lake** format. Not to be confused with [[Delta Live Tables]].
There are two types of delta tables managed and unmanaged (external).

## [[Managed]] Delta Tables
- **Definition**: In a **managed table**, Databricks takes full control of both the **data storage** and **metadata** associated with the table.
- **Storage**: The data is stored in the **Databricks File System (DBFS)** or a location that Databricks manages internally (like an S3 bucket or Azure Blob Storage under Databricks' control).
- **Lifecycle Management**: When you create a managed Delta Table, you don't have to worry about specifying the file path. If you drop or delete the table, the underlying data files are also deleted automatically by Databricks.
- **Use Case**: Managed tables are typically used when you want Databricks to handle all aspects of table management, including storage, metadata, and cleanup.

#### [[Unmanaged (External)]] Delta Tables

- **Definition**: An **unmanaged** (or **external**) table is where you provide a specific file path for the table’s data. While Databricks manages the metadata, the underlying data storage is managed separately by the user.
- **Storage**: The data files are stored in a specified location (like your S3 bucket, Azure Data Lake, or any other file system). Databricks only keeps track of the metadata for the table, not the actual files.
- **Lifecycle Management**: If you drop the table, Databricks will remove the metadata but **will not delete the underlying data files**. You must manually manage data cleanup.
- **Use Case**: Unmanaged tables are used when you want more control over where the data is stored, or if you want to share the data files across different systems.