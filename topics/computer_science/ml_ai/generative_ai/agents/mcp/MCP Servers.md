---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-03-28T14:43
modified: 2025-11-11T14:52
published:
sources:
  - "[MCP Server](https://modelcontextprotocol.io/sdk/java/mcp-server), [OpenAI SDK MCP](https://openai.github.io/openai-agents-python/mcp/), [MCP Spec Server Features](https://spec.modelcontextprotocol.io/specification/2025-03-26/server/)"
topics:
  - MCP
authors:
ai-assisted:
hidden:
public: true
---
# MCP Servers
 [MCP Server](https://modelcontextprotocol.io/sdk/java/mcp-server):
> The MCP Server is a foundational component in the Model Context Protocol (MCP) architecture that provides tools, resources, and capabilities to clients. It implements the server-side of the protocol, responsible for:
> - Exposing tools that clients can discover and execute
> - Managing resources with URI-based access patterns
> - Providing prompt templates and handling prompt requests
> - Supporting capability negotiation with clients
> - Implementing server-side protocol operations
> - Managing concurrent client connections
> - Providing structured logging and notifications
## Custom Servers
People are writing custom servers for the MCP protocol to support additional data sources or software.
**Sites for listing MCP servers:**
 - [[MCP.so]] - [wbesite](https://mcp.so/)
 - [[disco.dev]]
	 - https://disco.dev/
 - [Glama](https://glama.ai/mcp/servers?attributes=)
**Examples of Custom servers**:
- [Blender MCP](https://github.com/VxASI/blender-mcp-vxai/tree/main)
- [AWS S3 MCP](https://github.com/samuraikun/aws-s3-mcp)
- [[The AWS MCP Server is now generally available]] ([Link](https://aws.amazon.com/blogs/aws/the-aws-mcp-server-is-now-generally-available/))
	- 2026-05-06 — Managed remote MCP server giving agents authenticated access to all AWS APIs via `call_aws`, `search_documentation`, `read_documentation`, and `run_script` (sandboxed Python)
- [[New in Claude Managed Agents self-hosted sandboxes and MCP tunnels]] ([Link](https://claude.com/blog/claude-managed-agents-updates))
	- 2026-05-19 — MCP tunnels (research preview) let Claude Managed Agents reach private MCP servers via a single outbound gateway without exposing them publicly; paired with self-hosted sandboxes for in-perimeter tool execution
## Server Types
 [OpenAI SDK MCP](https://openai.github.io/openai-agents-python/mcp/):
Currently, the MCP spec defines two kinds of servers, based on the transport mechanism they use:
- **stdio** servers run as a subprocess of your application. You can think of them as running "locally".
	- `mcp.run(transport="stdio")`
- **HTTP over** **SSE** (Server-Sent Events) servers run remotely. You connect to them via a URL.
	- `mcp.run(transport="sse")`
## Server Features
[MCP Spec Server Features](https://spec.modelcontextprotocol.io/specification/2025-03-26/server/):
MCP servers provide three primitives with which LMMs can interact:

| Primitive  | Control            | Description                                           | Example                   |
|----------|-------------------|---------------------------------------------------|-------------------------|
| Prompts  | User-controlled    | Interactive templates invoked by user choice       | Slash commands, menu options |
| Resources| Application-controlled | Contextual data attached and managed by the client | File contents, git history    |
| Tools    | Model-controlled   | Functions exposed to the LLM to take actions       | API POST requests, file writing |

## Patterns
- [[MCP Server Patterns]] ([Link](https://arxiv.org/abs/2606.30317))
	- 2026-07-05 — catalogs five recurring server patterns (Resource Gateway, Tool Orchestrator, Stateful Session Server, Proxy Aggregator, Domain-Specific Adapter) plus four anti-patterns
