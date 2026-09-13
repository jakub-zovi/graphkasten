---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:51
published:
sources:
  - "[OTel Collector Docs](https://opentelemetry.io/docs/collector/)"
  - "[OTel Operator for Kubernetes](https://opentelemetry.io/docs/platforms/kubernetes/operator/)"
topics:
  - OpenTelemetry
  - Observability
  - Kubernetes
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# OTel Collector
- Standalone service that receives, processes, and exports telemetry data ([OTel Collector Docs](https://opentelemetry.io/docs/collector/))
- Acts as a vendor-agnostic pipeline between your instrumented services and storage backends
- Does **not** store data — it's a router and transformer

## Architecture
- Three pipeline stages
	- **Receivers** — accept incoming telemetry (OTLP, Jaeger, Zipkin, Prometheus scrape, etc.)
	- **Processors** — transform data (filter, sample, enrich with metadata, redact PII)
	- **Exporters** — forward to backends (Tempo, Loki, Prometheus, Datadog, stdout)
- Multiple pipelines can run simultaneously (one for traces, one for metrics, one for logs)

## Deployment Modes

### Agent Mode
- Collector runs as a sidecar or DaemonSet on every node
- Services send telemetry to local collector — low latency, no network hop
- Best for: production K8s clusters

### Gateway Mode
- Centralized collector(s) behind a load balancer
- Services send to the gateway; gateway fans out to multiple backends
- Best for: cross-cluster aggregation, central processing, multi-backend fan-out

### Combined (recommended)
- Agent collectors on each node forward to a Gateway collector
- Agents handle local buffering; Gateway handles routing and processing

```
[Service A]──┐             ┌──► Tempo
[Service B]──┼──► Agent ──► Gateway ──► Prometheus
[Service C]──┘             └──► Loki
```

## Kubernetes Deployment

### DaemonSet (Agent)
- One collector pod per node, deployed as a K8s DaemonSet
- Services send via `localhost` or node IP

### OpenTelemetry Operator
- K8s operator that manages Collector CRDs and auto-instruments pods ([OTel Operator Docs](https://opentelemetry.io/docs/platforms/kubernetes/operator/))
- Add annotation to a pod → operator injects OTel SDK automatically
	```yaml
	instrumentation.opentelemetry.io/inject-python: "true"
	```
- Manages `OpenTelemetryCollector` custom resources declaratively

## Why Use a Collector Instead of Direct Export
- **Decoupling** — swap backends without changing app code
- **Batching & retry** — app doesn't block on telemetry delivery failures
- **Sampling** — drop low-value traces before they reach storage (cost control)
- **Fan-out** — send same signal to multiple backends simultaneously
- **Sensitive data** — scrub PII/secrets centrally before export
