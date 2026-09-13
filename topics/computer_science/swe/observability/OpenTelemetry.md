---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-06-02T09:24
published:
sources:
  - "[OpenTelemetry Docs](https://opentelemetry.io/docs/)"
topics:
  - OpenTelemetry
  - Observability
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# OpenTelemetry
- Vendor-neutral, CNCF standard for instrumenting, collecting, and exporting telemetry data ([OpenTelemetry Docs](https://opentelemetry.io/docs/))
- Covers all three observability pillars: logs, metrics, and traces
- **Does not store or visualize data** — it is purely an instrumentation and transport layer
- Emerged from the merger of OpenCensus and OpenTracing (2019)

## What OTel Provides
- **APIs** — language-agnostic interfaces for emitting telemetry
- **SDKs** — language-specific implementations of the API
- **Instrumentation libraries** — auto-instrumentation for popular frameworks
- **OTel Collector** — standalone pipeline service for receiving, processing, exporting
- **OTLP** — standardized wire protocol (gRPC port 4317, HTTP port 4318)

## Why It Matters
- Before OTel: each vendor (Datadog, Jaeger, Zipkin, AWS X-Ray) had its own agent and SDK
	- Switching backends required re-instrumenting all application code
- With OTel: instrument once → point Collector at any backend
	- Swap Tempo for Jaeger, add Datadog alongside — zero app code changes

## Signal Types
- **Traces** — end-to-end request journeys (see [[Spans and Traces]])
- **Metrics** — numeric measurements over time (counters, gauges, histograms)
- **Logs** — structured/unstructured event records (OTel log support is newer, still maturing)
- **Profiles** — continuous profiling (in development as of 2025)

## Topics
- [[OTel SDK and Instrumentation]]
	- Language SDKs, auto-instrumentation, manual instrumentation, OTLP wire format
- [[OTel Collector]]
	- Standalone pipeline: agent vs gateway deployment, K8s DaemonSet, OTel Operator, processors

## TLDR
A useful mental model is:

> **OpenTelemetry is the plumbing, not the observability platform.**

It standardizes how telemetry is produced and transported, but something else must store, query, and visualize that data.
## The Big Picture

Imagine a request hitting your application:

```text
User Request
     │
     ▼
 Application
     │
     ├─ Trace data
     ├─ Metrics
     └─ Logs
     │
     ▼
 OpenTelemetry SDK
     │
     ▼
 OpenTelemetry Collector
     │
     ▼
 Backend(s)
     ├─ Tempo / Jaeger (traces)
     ├─ Prometheus / Mimir (metrics)
     ├─ Loki / Elasticsearch (logs)
     └─ Datadog / New Relic / Honeycomb
```

OTel sits in the middle:

```text
Application  →  OTel  →  Observability Backend
```
## What Problem OTel Actually Solves

Before OTel, every observability vendor had its own SDK:

```text
Application
 ├─ Datadog SDK
 ├─ New Relic SDK
 ├─ AWS X-Ray SDK
 └─ Zipkin SDK
```

If you switched vendors:

```text
Datadog → New Relic
```

you often had to:

* uninstall one agent
* rewrite instrumentation
* change trace propagation formats
* update dashboards and exporters

OTel changed this to:

```text
Application
     │
 OTel SDK
     │
 Collector
     │
 ├─ Datadog
 ├─ Tempo
 ├─ Jaeger
 └─ New Relic
```

The application only knows OTel.