---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-03-05T14:03
modified: 2026-03-05T14:05
published:
sources:
  - "[MCP Architecture](https://modelcontextprotocol.io/docs/learn/architecture)"
topics:
  - MCP
authors:
ai-assisted:
hidden:
public: true
---
# MCP Architecture
- The key participants in the MCP architecture are ([MCP Architecture](https://modelcontextprotocol.io/docs/learn/architecture)):
	- **[[MCP Host]]**: The AI application that coordinates and manages one or multiple MCP clients
	- **[[MCP Client]]**: A component that maintains a connection to an MCP server and obtains context from an MCP server for the MCP host to use
	- **[[MCP Server]]**: A program that provides context to MCP clients
![[mcp_architecture.png]]


