---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:46
published:
sources:
  - "[OTel Distributed Tracing](https://opentelemetry.io/docs/concepts/signals/traces/)"
  - "[W3C Trace Context](https://www.w3.org/TR/trace-context/)"
topics:
  - Distributed Tracing
  - Observability
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Distributed Tracing
- Technique for tracking a single request as it flows through multiple services in a distributed system
- Answers: which service is slow? Where did this error originate? What is the call graph?
- Essential for microservices architectures where a single user action touches many services

## Topics
- [[Spans and Traces]]
	- Trace and span data model, span kinds, attributes, sampling strategies
- [[Context Propagation]]
	- W3C traceparent header, B3/Jaeger formats, baggage, cross-service linking

## The Problem It Solves
- In a monolith, a stack trace shows the full call path
- In microservices, a request might hit API → Auth → Inventory → Payment → Notification
	- Each service has its own logs — correlating them manually is nearly impossible
	- Distributed tracing stitches them into a single visual timeline

## Core Data Model
- A **trace** is a directed acyclic graph (tree) of **spans**
- Each service creates spans; they're linked via `traceId` and `parentSpanId`
- The full trace is assembled by the backend (Tempo, Jaeger) by joining on `traceId`

## Instrumentation Requirements
- Each service must
	1. Extract incoming trace context from request headers
	2. Create a child span for its own work
	3. Inject trace context into all outbound requests
- OTel SDKs handle this automatically via auto-instrumentation

## Key Backends
- **Grafana Tempo** — object storage backed, TraceQL, Grafana-native
- **Jaeger** — CNCF project, older but widely deployed
- **Zipkin** — one of the original tracing systems, simpler feature set
- **Datadog APM**, **AWS X-Ray**, **Honeycomb** — commercial options