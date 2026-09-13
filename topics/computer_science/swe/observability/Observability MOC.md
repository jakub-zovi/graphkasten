---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-06-02T09:21
published:
sources:
  - "[OpenTelemetry Docs](https://opentelemetry.io/docs/)"
  - "[Grafana LGTM Stack](https://grafana.com/go/webinar/getting-started-with-grafana-lgtm-stack/)"
topics:
  - Observability
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Observability
- Ability to understand the internal state of a system byw examining its external outputs
- Three pillars: **logs** (events), **metrics** (measurements), **traces** (request journeys)
- Critical for operating distributed/microservice systems in production

## Three Pillars
- **Logs** — discrete timestamped events; what happened and when
	- Structured (JSON) logs are far more queryable than plain text
- **Metrics** — numeric time-series data; aggregated measurements over time
	- e.g. request rate, error rate, CPU %, p99 latency
- **Traces** — end-to-end request path across services; the call graph with timings
	- Answer: which service caused this 2s latency?

## The LGTM + OTel Architecture
```
Your Services
  │ (OTel SDK — auto or manual instrumentation)
  ▼
Grafana Alloy / OTel Collector
  │
  ├──► Loki       (logs)      ──┐
  ├──► Mimir      (metrics)   ──┤──► Grafana (unified UI)
  └──► Tempo      (traces)    ──┘
```
- [[OpenTelemetry]] — instrumentation standard; vendor-neutral SDK + Collector
- [[LGTM Stack]] — Grafana's storage and visualization stack

## Sections
- [[OpenTelemetry]]
	- Vendor-neutral instrumentation standard; SDK, OTel Collector, OTLP protocol
- [[LGTM Stack]]
	- Loki + Grafana + Tempo + Mimir; deployment via Helm, Grafana Alloy
- [[Distributed Tracing]]
	- Spans, traces, context propagation across services
