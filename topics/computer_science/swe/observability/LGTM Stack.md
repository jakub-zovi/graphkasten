---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:52
published:
sources:
  - "[Grafana LGTM Stack Overview](https://grafana.com/go/webinar/getting-started-with-grafana-lgtm-stack/)"
  - "[Grafana Alloy Docs](https://grafana.com/docs/alloy/latest/)"
  - "[kube-prometheus-stack Helm Chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)"
topics:
  - Observability
  - LGTM Stack
  - Kubernetes
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# LGTM Stack
- Grafana's open-source observability stack covering all three pillars ([Grafana LGTM Stack Overview](https://grafana.com/go/webinar/getting-started-with-grafana-lgtm-stack/))
- **L** — Loki (logs)
- **G** — Grafana (visualization)
- **T** — Tempo (traces)
- **M** — Mimir or Prometheus (metrics)

## How the Components Fit Together
```
Your Services (instrumented with OTel SDK)
        │
        ▼
  Grafana Alloy / OTel Collector
  ┌─────┬──────┬──────┐
  ▼     ▼      ▼      ▼
Loki  Tempo  Mimir  (other)
  └─────┴──────┴──────┘
              │
           Grafana
        (unified UI)
```
- Alloy/Collector is the single ingestion point — services don't talk to backends directly
- Grafana queries all backends as data sources and correlates across them

## Grafana Alloy
- Modern replacement for Promtail, Grafana Agent, and partially OTel Collector ([Grafana Alloy Docs](https://grafana.com/docs/alloy/latest/))
- Single binary that collects logs, metrics, traces, and profiles
- Configuration in River/Alloy language (HCL-inspired)
- Can forward to any LGTM backend or any OTLP-compatible destination
- Replaces the need to run separate Promtail + OTel Collector agents in K8s

## Kubernetes Deployment

### Helm Charts
- **`grafana/lgtm-distributed`** — full distributed LGTM stack (production-grade, microservices mode)
- **`grafana/grafana`** — standalone Grafana
- **`prometheus-community/kube-prometheus-stack`** — Prometheus + Grafana + Alertmanager + exporters ([kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack))
- **`grafana/alloy`** — Grafana Alloy as DaemonSet collector

### Typical Production Setup
1. Alloy as DaemonSet — collects node logs, scrapes pod metrics, receives OTLP traces
2. Loki as StatefulSet or Mimir/Tempo in distributed mode
3. Grafana as Deployment with persistent dashboard storage
4. Object storage (S3/MinIO) as the backing store for Loki, Tempo, Mimir

### Grafana Cloud Alternative
- Grafana Labs hosts the full LGTM stack as a managed service
- Free tier available; services write to Grafana Cloud via OTLP or remote_write

## Data Flow Per Signal
| Signal | Collector | Storage | Query |
|---|---|---|---|
| Logs | Alloy / Promtail | Loki | LogQL |
| Metrics | Alloy / Prometheus scrape | Mimir / Prometheus | PromQL |
| Traces | Alloy / OTel Collector | Tempo | TraceQL |

## Topics
- [[Prometheus]]
	- Pull-based metrics collection, PromQL, Alertmanager, Grafana Mimir for scale
- [[Grafana Loki]]
	- Label-indexed log aggregation, LogQL, Promtail/Alloy shipping
- [[Grafana Tempo]]
	- Object-storage trace backend, TraceQL, trace-to-logs/metrics correlation
- [[Grafana]]
	- Visualization layer, dashboards, Explore, cross-pillar correlations, alerting
