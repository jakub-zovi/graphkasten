---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:29
published:
sources:
  - "[OTel Context Propagation](https://opentelemetry.io/docs/concepts/context-propagation/)"
  - "[W3C Trace Context Spec](https://www.w3.org/TR/trace-context/)"
topics:
  - Distributed Tracing
  - Observability
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Context Propagation
- Mechanism for passing trace context (traceId, spanId) across process boundaries ([OTel Context Propagation](https://opentelemetry.io/docs/concepts/context-propagation/))
- Without propagation, each service would start a new independent trace — no end-to-end visibility

## How It Works
1. Service A starts a span, holds `traceId` + `spanId` in local context
2. Before making an outbound HTTP/gRPC call, A **injects** context into the request headers
3. Service B receives the request, **extracts** context from headers
4. B creates a new child span using A's `spanId` as `parentSpanId` and the same `traceId`
5. The two spans are now linked in the same trace tree

## W3C Trace Context (`traceparent`)
- Standard HTTP header for trace propagation ([W3C Trace Context Spec](https://www.w3.org/TR/trace-context/))
- Format: `traceparent: 00-{traceId}-{parentSpanId}-{flags}`
	- `00` — version
	- `traceId` — 32 hex chars (128-bit)
	- `parentSpanId` — 16 hex chars (64-bit)
	- `flags` — `01` = sampled, `00` = not sampled
- Example
	```
	traceparent: 00-4bf92f3577b34da6a3ce929d0e0e4736-00f067aa0ba902b7-01
	```
- `tracestate` header — optional vendor-specific metadata alongside `traceparent`

## Propagation Formats
| Format | Header | Notes |
|---|---|---|
| W3C Trace Context | `traceparent` | OTel default, modern standard |
| B3 (Zipkin) | `X-B3-TraceId`, `X-B3-SpanId` | Legacy, widely supported |
| Jaeger | `uber-trace-id` | Jaeger-specific |
| AWS X-Ray | `X-Amzn-Trace-Id` | AWS services |

- OTel supports multiple propagators simultaneously — useful when integrating with legacy services

## Baggage
- Alongside trace context, OTel allows propagating arbitrary key-value **baggage**
- Propagated via `baggage` HTTP header
- Use case: pass `user.id` or `tenant.id` through the whole call chain for log correlation
- Warning: baggage is sent with every outbound request — keep it small
