---
tags:
  - cs
  - cs/data_eng
created: 2026-03-14T00:00
modified: 2026-07-26T13:27
published:
sources:
  - "[dbt Documentation](https://docs.getdbt.com/)"
topics:
  - Data Transformation
  - ELT
  - SQL Modeling
authors:
ai-assisted: true
hidden:
public: true
human-review: true
banner: https://janzednicek.cz/wp-content/uploads/2024/02/dbt5596.jpg
---
# dbt (data build tool)
- dbt is an open-source **SQL transformation framework** — the **T** in ELT. It lets data analysts and engineers write modular SQL `SELECT` statements (called **models**) and handles compilation, dependency resolution, testing, and documentation.
- dbt does **not** move data. It connects to a warehouse and runs SQL inside it.

## Core Concepts

### Models
A model is a `.sql` file containing a single `SELECT` statement. dbt compiles it into a `CREATE TABLE/VIEW AS SELECT …` and executes it in the warehouse.

```sql
-- models/staging/stg_orders.sql
SELECT
    id AS order_id,
    user_id,
    status,
    created_at
FROM {{ source('raw', 'orders') }}
```

Reference another model with `{{ ref('model_name') }}`:
```sql
-- models/marts/fct_orders.sql
SELECT
    o.order_id,
    u.full_name,
    o.status
FROM {{ ref('stg_orders') }} o
JOIN {{ ref('stg_users') }} u ON o.user_id = u.user_id
```

### Materialization Strategies
Controls how dbt persists the model result:

| Strategy | Behaviour | When to use |
|---|---|---|
| `view` | Creates a SQL view (default) | Lightweight, always fresh |
| `table` | Drops and recreates a table on each run | Frequently queried; expensive views |
| `incremental` | Inserts/updates only new rows | Large tables; append-heavy data |
| `ephemeral` | No physical object; inlined as a CTE | Reusable logic, not queried directly |

```sql
-- models/marts/fct_events.sql
{{ config(materialized='incremental', unique_key='event_id') }}

SELECT *
FROM {{ ref('stg_events') }}
{% if is_incremental() %}
WHERE created_at > (SELECT MAX(created_at) FROM {{ this }})
{% endif %}
```

### Sources
Declare raw tables as **sources** in `schema.yml`:
```yaml
sources:
  - name: raw
    tables:
      - name: orders
      - name: users
```

### Lineage Graph
dbt auto-generates a DAG of model dependencies, viewable in the docs site:
```bash
dbt docs generate
dbt docs serve  # opens browser at localhost:8080
```

## CLI Commands
```bash
dbt run                        # compile + execute all models
dbt run --select stg_orders    # run a single model
dbt run --select +fct_orders   # run model + all its upstream dependencies
dbt test                       # run all tests
dbt build                      # run + test in dependency order
dbt compile                    # compile SQL without executing
dbt source freshness           # check source table staleness
```

## SQL & Jinja Templating
dbt uses **standard SQL** — no proprietary dialect. Jinja is a preprocessing layer compiled away before the warehouse executes anything.

Key Jinja functions:
- `{{ ref('model_name') }}` — resolves dependency and builds the lineage DAG
- `{{ source('schema', 'table') }}` — references raw source tables
- `{% if is_incremental() %}` — conditional logic compiled out at runtime

**Adapters** translate compiled SQL to the target dialect: `dbt-snowflake`, `dbt-bigquery`, `dbt-spark`, `dbt-databricks`, `dbt-duckdb`, `dbt-postgres`. The same model code runs against different engines with minimal config change.

## Deployment / Where It Runs
dbt **connects to** the warehouse — it does not run inside it.

### dbt Core (OSS)
- Runs wherever Python runs: local machine, CI/CD runner, container
- No server required; invoked via CLI
- Common in CI/CD pipelines:
```yaml
# GitHub Actions example
- name: Run dbt
  run: |
    dbt deps
    dbt build
  env:
    DBT_PROFILES_DIR: ./profiles
```

### dbt Cloud
- Managed SaaS by dbt Labs
- Provides: web IDE, job scheduler, docs hosting, CI/CD integration
- Connects to the warehouse via credentials stored in the UI
### In Kubernetes
- dbt runs inside a pod, triggered by [[Airflow]] (via `BashOperator` or `astronomer-cosmos`) or a CI/CD job
- No persistent dbt server; the pod exits after the run
### Supported Warehouses (adapters)
dbt connects to the warehouse via adapters — it does **not** run queries itself:
- Snowflake (`dbt-snowflake`)
- BigQuery (`dbt-bigquery`)
- Redshift (`dbt-redshift`)
- Databricks (`dbt-databricks`)
- DuckDB (`dbt-duckdb`) — popular for local development
- Postgres (`dbt-postgres`)

## Relationship with Airflow
- [[Airflow]] orchestrates **when** dbt runs; dbt handles **what** the SQL transformations are.
	- Airflow triggers `dbt run` / `dbt build` as a task
	- `astronomer-cosmos` maps each dbt model to an individual Airflow task for fine-grained observability and retries
## Disadvantages
- It is SQL based 
- Doesn't have debugging functionality
- dbt is just a T