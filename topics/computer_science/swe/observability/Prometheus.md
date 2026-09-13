---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:52
published:
sources:
  - "[Prometheus Docs](https://prometheus.io/docs/introduction/overview/)"
  - "[Grafana Mimir Docs](https://grafana.com/docs/mimir/latest/)"
topics:
  - Observability
  - Metrics
  - LGTM Stack
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Prometheus
- Open-source metrics collection and time-series database ([Prometheus Docs](https://prometheus.io/docs/introduction/overview/))
- Pull-based model — Prometheus scrapes `/metrics` HTTP endpoints from services on a schedule
- De facto standard for metrics in cloud-native / Kubernetes environments

## Core Concepts
- **Time series** — stream of timestamped float64 values identified by metric name + label set
	- e.g. `http_requests_total{method="GET", status="200"} 1234`
- **Labels** — key-value pairs that differentiate dimensions of a metric
- **Scrape interval** — how often Prometheus polls each target (default: 15s)
- **Retention** — local storage, typically 15 days; use Mimir/Thanos for long-term

## Metric Types
- **Counter** — monotonically increasing value (request count, error count)
- **Gauge** — value that can go up and down (CPU %, memory, queue depth)
- **Histogram** — samples observations into buckets (request latency, payload size)
- **Summary** — similar to histogram but calculates quantiles client-side

## PromQL
- Powerful query language for selecting and aggregating time series
- Examples
	- `http_requests_total` — all time series for this metric
	- `rate(http_requests_total[5m])` — per-second rate over last 5 minutes
	- `histogram_quantile(0.99, rate(http_request_duration_seconds_bucket[5m]))` — p99 latency

## Alertmanager
- Companion service that handles alerts fired by Prometheus
- Groups, deduplicates, and routes alerts to receivers (Slack, PagerDuty, email, etc.)
- Supports inhibition (silence child alerts when parent is firing) and silences

## Grafana Mimir
- Horizontally scalable, long-term storage for Prometheus metrics ([Grafana Mimir Docs](https://grafana.com/docs/mimir/latest/))
- Drop-in Prometheus-compatible API — same PromQL, same remote_write
- Stores metrics in object storage (S3, GCS) — far cheaper than local SSD
- The **M** in the LGTM stack (replaces standalone Prometheus for production scale)

## Kubernetes Integration
- `kube-state-metrics` — exposes K8s object state as Prometheus metrics
- `node-exporter` — exposes hardware/OS metrics per node
- `ServiceMonitor` / `PodMonitor` CRDs (via Prometheus Operator) — declarative scrape config
