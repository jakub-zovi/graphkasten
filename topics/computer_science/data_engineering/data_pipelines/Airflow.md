---
tags:
  - cs
  - cs/data_eng
created: 2026-03-14T00:00
modified: 2026-07-26T10:46
published:
sources:
  - "[Apache Airflow Documentation](https://airflow.apache.org/docs/)"
topics:
  - Workflow Orchestration
  - DAGs
  - Executors
authors:
ai-assisted: true
hidden:
public: true
human-review: true
banner: https://upload.wikimedia.org/wikipedia/commons/7/71/AirflowLogo.svg
---
# Apache Airflow
- Apache Airflow is an open-source **workflow orchestration platform** for authoring, scheduling, and monitoring data pipelines. Pipelines are defined as **DAGs** (Directed Acyclic Graphs) in Python — code is the source of truth.
- Originally created at Airbnb (2014), donated to Apache in 2016.
## Core Concepts

### DAG (Directed Acyclic Graph)
- A DAG is a Python file defining a collection of tasks and their dependencies. **Tasks flow in one direction — no cycles**.

```python
from airflow import DAG
from airflow.operators.bash import BashOperator
from datetime import datetime

with DAG(
    dag_id="example_dag",
    start_date=datetime(2025, 1, 1),
    schedule="@daily",
    catchup=False,
) as dag:
    extract = BashOperator(task_id="extract", bash_command="python extract.py")
    transform = BashOperator(task_id="transform", bash_command="python transform.py")
    load = BashOperator(task_id="load", bash_command="python load.py")

    extract >> transform >> load  # dependency chain
```

### Tasks & Operators
- A **Task** is a unit of work. An **Operator** defines what it does:
	- `PythonOperator` — run a Python callable
	- `BashOperator` — run a shell command
	- `PostgresOperator` — execute SQL
	- `KubernetesPodOperator` — spin up a k8s pod
	- `DbtTaskGroup` — run dbt models (via `airflow-dbt` or `astronomer-cosmos`)

### Scheduler
- The Scheduler continuously parses DAG files, triggers tasks when dependencies are met, and submits them to the Executor.

### Executor
- Executors control how and where tasks run:

| Executor | Description |
|---|---|
| `SequentialExecutor` | One task at a time; dev/testing only |
| `LocalExecutor` | Parallel tasks on the same machine |
| `CeleryExecutor` | Distributes tasks to Celery workers; needs Redis/RabbitMQ as broker |
| `KubernetesExecutor` | Each task runs in its own k8s pod; fully ephemeral |
| `CeleryKubernetesExecutor` | Hybrid: some tasks on Celery, heavy tasks on k8s pods |

## Integration with dbt
- [[dbt]] **handles SQL transformations; Airflow orchestrates when they run.**

```python
from airflow.operators.bash import BashOperator

dbt_run = BashOperator(
    task_id="dbt_run",
    bash_command="dbt run --profiles-dir /profiles --project-dir /dbt",
)
```

Or use `astronomer-cosmos` for a richer integration that maps each dbt model to an Airflow task:
```python
from cosmos import DbtTaskGroup, ProjectConfig, ProfileConfig

dbt_tg = DbtTaskGroup(
    project_config=ProjectConfig("/dbt"),
    profile_config=ProfileConfig(...),
)
```
