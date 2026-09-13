---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-03-29T17:39
modified: 2026-07-26T13:33
published:
sources:
  - "[What is A2A?](https://a2a-protocol.org/latest/topics/what-is-a2a/)"
  - "[Agentic Web - arxiv 2507.21206](https://arxiv.org/pdf/2507.21206)"
topics:
  - Agent Communication
  - Agent Protocol
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# A2A Request Lifecycle
([What is A2A?](https://a2a-protocol.org/latest/topics/what-is-a2a/))
## 4-Phase Lifecycle
### Phase 1: Agent Discovery
- Client sends `GET /.well-known/agent-card` to retrieve the remote agent's [[A2A Key Concepts#Agent Card|Agent Card]]
- Client evaluates skills and capabilities listed in the Agent Card to confirm the agent matches task requirements
### Phase 2: Authentication
- Client parses `securitySchemes` from the Agent Card
- If OpenID Connect: client requests a JWT from the Auth Server
- Auth Server returns a signed JWT; client attaches it to subsequent requests via HTTP headers
### Phase 3: `sendMessage` (Synchronous / Polling)
- Client parses the endpoint URL from the Agent Card
- Client sends `POST /sendMessage` with JWT
- Server processes the request, creates a Task, and returns a **Task Response**
- For long-running operations, the client periodically polls the server for task status updates
### Phase 4: `sendMessageStream` (Streaming)
- Client sends `POST /sendMessageStream` with JWT
- Server opens a **Server-Sent Events (SSE)** connection and streams multiple events:
	1. `Task Submitted`
	2. `TaskStatusUpdateEvent` (progress)
	3. `TaskArtifactUpdateEvent` (incremental artifact delivery)
	4. `TaskStatusUpdateEvent: Completed`
- Client can subscribe to receive these updates in real time without polling
## Interaction Mechanisms Summary
([What is A2A?](https://a2a-protocol.org/latest/topics/what-is-a2a/))
- **Request/Response (Polling)** — synchronous request; client polls server for updates on long-running tasks
- **Server-Sent Events (SSE)** — client opens a stream to receive real-time incremental results over a persistent HTTP connection
- **Push Notifications** — server actively sends asynchronous webhook notifications to the client for extended or disconnected scenarios
## Workflow (High-Level)
([Agentic Web 2507.21206](https://arxiv.org/pdf/2507.21206))
1. Client agent receives user query and creates a new **Task** with a unique ID
2. Client retrieves **Agent Cards** to identify remote agents matching task requirements
3. Client and remote agents exchange **Messages** under the A2A protocol
4. **Task** state is continuously updated as execution progresses
5. Once complete, output is encapsulated and delivered as an **Artifact**
