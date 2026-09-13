---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-03-29T17:39
modified: 2026-07-26T13:32
published:
sources:
  - "[What is A2A?](https://a2a-protocol.org/latest/topics/what-is-a2a/)"
  - "[A2A Key Concepts](https://a2a-protocol.org/latest/topics/key-concepts/)"
  - "[Agentic Web - arxiv 2507.21206](https://arxiv.org/pdf/2507.21206)"
topics:
  - Agent Communication
  - Multi-Agent Systems
  - Agent Protocol
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# A2A Protocol
- A2A (Agent-to-Agent) is an open standard proposed by Google for enterprise-scale agent ecosystems
- Enables seamless communication and collaboration between AI agents, irrespective of their underlying frameworks or provider-specific implementations
- Now governed under the **Linux Foundation** (Apache 2.0)
- Github: [a2aproject/A2A](https://github.com/a2aproject/A2A)
	- **20k** stars
## Problems It Solves
([What is A2A?](https://a2a-protocol.org/latest/topics/what-is-a2a/))
- **Agent Misrepresentation** — developers wrap agents as simple tools, which is fundamentally limiting as it fails to capture the agent's full capabilities and reasoning potential
- **Custom Integration Overhead** — without standards, each agent interaction requires bespoke point-to-point solutions
- **Scalability Challenges** — systems become difficult to maintain as agent interactions multiply
- **Security Gaps** — ad hoc communication lacks consistent security measures
- **Limited Interoperability** — prevents organic formation of complex AI ecosystems
## Design Principles
([What is A2A?](https://a2a-protocol.org/latest/topics/what-is-a2a/))
- **Simplicity** — leverages existing standards (HTTP, JSON-RPC, SSE) rather than inventing new technologies
- **Enterprise Readiness** — incorporates authentication, authorization, security, privacy, tracing, and monitoring
- **Asynchronous Support** — natively handles long-running operations and streaming for disconnected agents
- **Modality Independent** — agents communicate using a wide variety of content types
- **Opaque Execution** — agents collaborate without exposing internal logic, memory, or proprietary tools
## Core Actors
([A2A Key Concepts](https://a2a-protocol.org/latest/topics/key-concepts/))

![|600](a2a-actors.png)

- **User** — end party initiating requests, either human or automated service
- **A2A Client (Client Agent)** — application, service, or another AI agent acting on behalf of the user
- **A2A Server (Remote Agent)** — exposes HTTP endpoints implementing A2A; operates as an opaque system, internal workings hidden from clients
## Agent Stack
([What is A2A?](https://a2a-protocol.org/latest/topics/what-is-a2a/))

![|600](a2a-agentic-stack.png)

- **A2A** — inter-organizational agent-to-agent communication
- **MCP** — model-to-data/resource connections (stateless tool integration)
- **Frameworks** — agent construction toolkits (ADK, LangGraph, Crew AI)
- **Models** — LLM reasoning foundation
## Topics
- [[A2A Key Concepts]]
	- Core data model: Agent Card, Task, Message, Part, Artifact, ContextId
- [[A2A Request Lifecycle]]
	- 4-phase request flow: discovery, authentication, message sending, streaming
- [[A2A vs MCP]]
	- Detailed comparison of A2A and MCP protocols
