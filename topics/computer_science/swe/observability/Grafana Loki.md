---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:51
published:
sources:
  - "[Grafana Loki Docs](https://grafana.com/docs/loki/latest/)"
topics:
  - Observability
  - Logs
  - LGTM Stack
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Grafana Loki
- Horizontally scalable log aggregation system, designed to be cost-effective ([Grafana Loki Docs](https://grafana.com/docs/loki/latest/))
- The **L** in the LGTM stack
- Key design decision: indexes only **labels/metadata**, not the full log content
	- Makes storage cheap (no inverted index over log text)
	- Trade-off: full-text search is slower than Elasticsearch

## Core Concepts
- **Log stream** — set of logs sharing the same label set (e.g. `{app="api", env="prod"}`)
- **Labels** — key-value pairs attached to a stream; the only indexed data
	- Keep cardinality low — don't use high-cardinality values (request IDs, user IDs) as labels
- **Chunks** — compressed log data stored in object storage (S3, GCS, filesystem)
- **Index** — maps label sets to chunk locations

## LogQL
- Query language for Loki, inspired by PromQL
- Two query types
	- **Log queries** — return log lines: `{app="api"} |= "error"`
	- **Metric queries** — derive metrics from logs: `rate({app="api"} |= "error" [5m])`
- Pipeline operators: `|=` (contains), `!=` (not contains), `|~` (regex), `| json` (parse JSON fields)

## Log Shipping
- **Promtail** — traditional agent, runs as DaemonSet, tails pod log files
- **Grafana Alloy** — modern replacement for Promtail (see [[LGTM Stack]])
- **OTel Collector** — can export logs to Loki via OTLP or Loki exporter
- **Docker / K8s** — Loki Docker driver plugin for container log collection

## vs Elasticsearch
| | Loki | Elasticsearch |
|---|---|---|
| Index | Labels only | Full text |
| Storage cost | Low (object storage) | High (inverted index) |
| Query speed | Slower on large text search | Faster full-text |
| Ops complexity | Low | High |
| Best for | Cloud-native, cost-sensitive | Enterprise full-text search |
