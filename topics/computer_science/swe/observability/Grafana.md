---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:47
published:
sources:
  - "[Grafana Docs](https://grafana.com/docs/grafana/latest/)"
topics:
  - Observability
  - LGTM Stack
  - Visualization
authors:
ai-assisted: true
hidden:
public: true
human-review: true
banner: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSX2QCPgGr9lsO8jzn_kizSYFw0rAaggw3YW7Nf1tzc-Wh6CRT7kJbhhQMG&s=10
---
# Grafana
- Open-source visualization and dashboarding platform ([Grafana Docs](https://grafana.com/docs/grafana/latest/))
- The **G** in the LGTM stack — the single UI layer over all observability backends
- Does not store data itself — queries data sources and renders results

## Data Sources
- Connects to any backend via data source plugins
	- Metrics: Prometheus, Mimir, Graphite, InfluxDB
	- Logs: Loki, Elasticsearch, CloudWatch Logs
	- Traces: Tempo, Jaeger, Zipkin, AWS X-Ray
	- Databases: PostgreSQL, MySQL, etc.
- Multiple data sources can be queried in a single dashboard

## Key Features

### Dashboards
- Panels arranged on a grid — each panel is a query + visualization
- Visualization types: time series, bar chart, stat, gauge, table, heatmap, geomap
- Variables — dynamic dropdowns that parameterize queries (e.g. select environment, service)
- Annotations — mark events on time series graphs (deployments, incidents)

### Explore
- Ad-hoc query interface without a pre-built dashboard
- Switch between data sources and query types fluidly
- Essential for incident investigation

### Correlations (the killer feature)
- **Trace to logs** — from a Tempo span, jump to Loki logs filtered to that service + time
- **Trace to metrics** — from a Tempo span, open Prometheus metrics for that service
- **Logs to traces** — from a Loki log line containing a `traceId`, jump to Tempo trace
- **Exemplars** — Prometheus data points linked to a specific trace ID

### Alerting
- Unified alerting across all data sources (Grafana 8+)
- Alert rules defined in dashboards or standalone
- Routes to Alertmanager, Slack, PagerDuty, email, OpsGenie, etc.

## Grafana Cloud vs Self-Hosted
- **Grafana Cloud** — managed SaaS, includes hosted Loki, Tempo, Mimir
- **Self-hosted** — deploy via Helm chart (`grafana/grafana`), Docker, or binary
- **Grafana Enterprise** — adds RBAC, data source permissions, reporting, auditing
