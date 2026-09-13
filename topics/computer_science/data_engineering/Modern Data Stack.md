---
tags:
  - cs
  - cs/data_eng
created: 2026-03-14T00:00
modified: 2026-07-26T13:28
published:
sources:
topics:
  - Modern Data Stack
  - Pipeline Architecture
  - Workflow Orchestration
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Modern Data Stack
- The modern data stack is a layered architecture that separates **orchestration**, **transformation**, and **compute** into distinct tools, each doing one thing well.

## Architecture
```
Airflow            ← when to run  (orchestration)
  └─ dbt           ← what SQL to run  (transformation middleware)
       └─ Snowflake / BigQuery / Spark   ← actual computation
```

## What Each Layer Does
| Layer                 | Responsibility                                          | What it does NOT do               |
| --------------------- | ------------------------------------------------------- | --------------------------------- |
| **[[Airflow]]**       | Schedule, retry, alert, fan-out                         | Zero data processing              |
| **[[dbt]]**           | Compile Jinja+SQL, resolve dependencies, submit queries | Zero computation — just sends SQL |
| **Warehouse / Spark** | Execute SQL, distributed joins, aggregations            | Zero scheduling logic             |

Airflow runs on a lightweight scheduler pod. dbt runs in a Python process. All heavy computation stays inside the warehouse or Spark cluster.

## dbt SQL & Jinja Templating
dbt uses **standard SQL** — there is no proprietary dialect. Jinja templating is a preprocessing layer compiled away before the warehouse sees any query.

Key Jinja functions:
- `{{ ref('model_name') }}` — resolves to the fully-qualified table/view name; builds the dependency DAG
- `{{ source('schema', 'table') }}` — references raw source tables declared in `schema.yml`
- `{% if is_incremental() %}` — conditional logic for incremental materialization

```sql
-- what you write
SELECT * FROM {{ ref('stg_orders') }}
WHERE {% if is_incremental() %} created_at > (SELECT MAX(created_at) FROM {{ this }}) {% endif %}

-- what the warehouse receives (compiled)
SELECT * FROM analytics.stg_orders
WHERE created_at > (SELECT MAX(created_at) FROM analytics.fct_orders)
```

**Adapters** translate compiled SQL to the target dialect:
- `dbt-snowflake`, `dbt-bigquery`, `dbt-redshift`
- `dbt-databricks` / `dbt-spark` — same dbt model code runs on Spark SQL
- `dbt-duckdb` — popular for local development

The result: one set of dbt models runs against different engines with minimal config change.

## Why Two DAGs?
Both Airflow and dbt have a concept of a DAG, but they operate at different scopes:

| | Airflow DAG | dbt DAG |
|---|---|---|
| **Scope** | Task-level orchestration | SQL model lineage |
| **Nodes** | Tasks (run script, call API, trigger dbt) | dbt models (stg_orders → fct_orders) |
| **Purpose** | What runs, when, in what order | Which SQL depends on which SQL |

With **`astronomer-cosmos`**: dbt's model DAG is unrolled into individual Airflow tasks (one task per dbt model), giving fine-grained retry and observability at the model level inside Airflow.

## Why These Tools Exist
**Before Airflow** — pipelines were cron jobs chained with `&&`:
- No retry on failure
- No visibility into what ran or failed
- No dependency tracking between jobs

**Before dbt** — transformations were 300 SQL scripts in a folder:
- No lineage (which table feeds which)
- No tests or data quality checks
- No modularity or reuse

## Spark / Hadoop Context
Spark solves a different problem: **data that doesn't fit on one machine**. It's a distributed compute engine, not a warehouse. Airflow can orchestrate Spark jobs via `SparkSubmitOperator` or Kubernetes pod operators. dbt can target Spark via `dbt-spark` / `dbt-databricks`.
