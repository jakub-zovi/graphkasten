---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:51
published:
sources:
  - "[Grafana Tempo Docs](https://grafana.com/docs/tempo/latest/)"
  - "[TraceQL Docs](https://grafana.com/docs/tempo/latest/traceql/)"
topics:
  - Observability
  - Distributed Tracing
  - LGTM Stack
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Grafana Tempo
- Distributed tracing backend — stores and queries traces at scale ([Grafana Tempo Docs](https://grafana.com/docs/tempo/latest/))
- The **T** in the LGTM stack
- Designed for cost-efficiency: stores traces in object storage (S3, GCS, Azure Blob)
	- No local SSD required for trace data

## Core Concepts
- Accepts traces in multiple formats: OTLP, Jaeger, Zipkin
- Stores full trace data (all spans) keyed by `traceId`
- Indexes only trace metadata for search (service name, span name, duration, tags)

## TraceQL
- Query language for searching traces ([TraceQL Docs](https://grafana.com/docs/tempo/latest/traceql/))
- Examples
	- `{ .service.name = "api" && duration > 500ms }` — slow spans in api service
	- `{ status = error }` — all error spans
	- `{ span.http.status_code = 500 }` — spans with HTTP 500
- Supports structural queries — e.g. find traces where a child span has an error

## Grafana Integration
- **Trace to logs** — click a span in Grafana → jump to Loki logs for that exact time window and service
- **Trace to metrics** — click a span → see Prometheus metrics for that service at that time
- **Service graph** — auto-generated topology map of service dependencies from trace data
- **RED metrics** — Rate, Errors, Duration automatically derived from traces

## Storage Architecture
- **Distributor** — receives incoming trace data, routes to ingesters
- **Ingester** — buffers recent traces in memory, flushes to object storage
- **Compactor** — merges and compacts blocks in object storage
- **Querier** — handles search queries, reads from ingesters + object storage

## vs Jaeger
| | Tempo | Jaeger |
|---|---|---|
| Storage backend | Object storage (S3/GCS) | Cassandra / Elasticsearch |
| Cost | Very low | Higher |
| Query language | TraceQL | JQL (basic) |
| Grafana integration | Native | Via data source plugin |
