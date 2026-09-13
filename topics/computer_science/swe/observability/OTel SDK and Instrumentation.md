---
tags:
  - cs
  - cs/swe
  - cs/swe/observability
created: 2026-04-14T17:00
modified: 2026-07-26T13:52
published:
sources:
  - "[OTel Language SDKs](https://opentelemetry.io/docs/languages/)"
  - "[OTel Instrumentation](https://opentelemetry.io/docs/concepts/instrumentation/)"
topics:
  - OpenTelemetry
  - Observability
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# OTel SDK and Instrumentation
- Language-specific libraries that instrument application code and emit telemetry ([OTel Language SDKs](https://opentelemetry.io/docs/languages/))
- Available for Python, Go, Java, JavaScript/Node, .NET, Ruby, Rust, PHP, and more
- The SDK is what runs inside your application process; the [OTel Collector](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fswe%2Fobservability%2FOTel%20Collector)runs outside

## Instrumentation Types

### Auto-Instrumentation
- Zero code changes — hooks into frameworks and libraries automatically
- Instruments HTTP servers/clients, DB drivers, message queues, gRPC, etc.
- Language-specific agents or monkey-patching
	- Python: `opentelemetry-instrument python app.py`
	- Java: `-javaagent:opentelemetry-javaagent.jar`
	- Node.js: `--require @opentelemetry/auto-instrumentations-node/register`
- Best for: getting started quickly, brownfield apps

### Manual Instrumentation
- Explicitly create spans and add attributes in code
	```python
	with tracer.start_as_current_span("my-operation") as span:
	    span.set_attribute("user.id", user_id)
	    result = do_work()
	```
- Best for: business logic context, custom attributes, fine-grained control

### Library Instrumentation
- Pre-built plugins for popular libraries (requests, sqlalchemy, flask, express, etc.)
- Import and register alongside the SDK

## SDK Components
- **TracerProvider** — factory for creating `Tracer` instances
- **MeterProvider** — factory for creating `Meter` instances (metrics)
- **LoggerProvider** — factory for creating `Logger` instances
- **Propagators** — handle context injection/extraction across process boundaries (see [Context Propagation](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fswe%2Fobservability%2FContext%20Propagation))
- **Exporters** — send data to Collector or directly to backends via OTLP

## OTLP (OpenTelemetry Protocol)
- The wire format used between SDK → Collector and Collector → backends
- Supported transports: gRPC (port 4317) and HTTP/protobuf (port 4318)
- Replaces vendor-specific wire formats (Jaeger Thrift, Zipkin JSON, etc.)
- All major backends now accept OTLP natively
