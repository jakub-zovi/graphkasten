---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:52
published:
sources:
  - "[OTel Traces Concepts](https://opentelemetry.io/docs/concepts/signals/traces/)"
topics:
  - Distributed Tracing
  - Observability
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Spans and Traces
- Core data model of distributed tracing ([OTel Traces Concepts](https://opentelemetry.io/docs/concepts/signals/traces/))

## Trace
- Represents the full end-to-end journey of a single request through a distributed system
- Composed of a tree of spans
- Identified by a globally unique **traceId** (128-bit / 16-byte hex string)
- All spans belonging to the same request share the same `traceId`

## Span
- Represents a single unit of work within a trace
- Fields
	- `traceId` — which trace this span belongs to
	- `spanId` — unique ID for this span (64-bit)
	- `parentSpanId` — ID of the parent span (empty for root span)
	- `name` — operation name (e.g. `GET /api/users`, `db.query`)
	- `startTime` / `endTime` — timestamps
	- `duration` — derived from start/end
	- `status` — `OK`, `ERROR`, `UNSET`
	- `kind` — `SERVER`, `CLIENT`, `PRODUCER`, `CONSUMER`, `INTERNAL`
	- `attributes` — key-value metadata (`http.method`, `db.statement`, `user.id`)
	- `events` — timestamped log-like messages within a span
	- `links` — references to spans in other traces (e.g. async jobs)

## Span Relationships
```
Trace (traceId: abc123)
└── [ROOT] HTTP POST /checkout  (spanId: 001, duration: 520ms)
    ├── Auth service call        (spanId: 002, parent: 001, duration: 12ms)
    ├── Inventory DB query       (spanId: 003, parent: 001, duration: 450ms)  ← bottleneck
    └── Payment service call     (spanId: 004, parent: 001, duration: 55ms)
```

## Span Attributes (Semantic Conventions)
- OTel defines standard attribute names to ensure consistency across languages/backends
	- HTTP: `http.method`, `http.status_code`, `http.url`
	- DB: `db.system`, `db.statement`, `db.name`
	- RPC: `rpc.system`, `rpc.service`, `rpc.method`
	- Messaging: `messaging.system`, `messaging.destination`

## Sampling
- Recording every span in high-traffic systems is expensive
- **Head-based sampling** — decision made at trace root (fast, simple)
	- Always-on, probabilistic (e.g. 10%), rate-limiting
- **Tail-based sampling** — decision made after full trace collected (can sample based on outcome)
	- Keep all error traces, sample 1% of successful traces
	- Requires buffering — typically done in the [OTel Collector](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fswe%2Fobservability%2FOTel%20Collector)
