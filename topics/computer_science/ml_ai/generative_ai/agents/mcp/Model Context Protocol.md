---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-02-21T15:17
modified: 2026-04-03T12:06
published:
sources:
  - "[Introducing the Model Context Protocol](https://www.anthropic.com/news/model-context-protocol)"
  - "[MCP Github](https://github.com/modelcontextprotocol)"
  - "[MCP Docs](https://modelcontextprotocol.io/introduction)"
  - "[Claude can now connect to your world](https://www.anthropic.com/news/integrations)"
topics:
  - MCP
authors:
ai-assisted:
hidden:
public: true
aliases:
  - MCP
---
# Model Context Protocol
- [MCP Docs](https://modelcontextprotocol.io/introduction):
> MCP is an open protocol that standardizes how applications provide context to LLMs. Think of MCP like a USB-C port for AI applications. Just as USB-C provides a standardized way to connect your devices to various peripherals and accessories, MCP provides a standardized way to connect AI models to different data sources and tools.
## Topics
- [[MCP Architecture]]
- [[MCP Primitives]]
- [[MCP Servers]]
## Spec Releases
- [[The 2026-07-28 MCP Specification Release Candidate]] ([Link](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/))
	- 2026-05-21 — RC for the next spec: stateless protocol core, Extensions framework, Tasks, MCP Apps, OAuth/OIDC-aligned authorization, formal deprecation policy
## Resources
- [[FastMCP]]
	- The fast, Pythonic way to build MCP servers and clients
	- Like FastAPI but for MCP
		- **So basically go to option for any project**
	- Many additional features such as Code Mode, Tool Search etc.
	- [jlowin/fastmcp](https://github.com/jlowin/fastmcp)
		- 23.2k stars
	- Resources
		- [Introducing FastMCP 3.0](https://www.jlowin.dev/blog/fastmcp-3)
- [[MCP - Interactive user interfaces]]
	- [MCP Apps: Extending servers with interactive user interfaces](https://blog.modelcontextprotocol.io/posts/2025-11-21-mcp-apps/)
- [[Test & debug MCP servers]]
	- https://www.mcpjam.com/
	- [MCPJam/inspector](https://github.com/MCPJam/inspector)
		- 1.4k stars
## Deprecated
### Criticism
- [GitHub MCP Exploited](https://invariantlabs.ai/blog/mcp-github-vulnerability)
- [OpenAI adds MCP support to Agents SDK | Hacker News](https://news.ycombinator.com/item?id=43485566)
- Originally no support for authentication and therefore limited support for remote MCP servers
### Remote MCP (With Auth)
- [Claude can now connect to your world](https://www.anthropic.com/news/integrations):
> Developers can also create their own Integrations in as little as 30 minutes using our documentation or solutions like Cloudflare that provide built-in OAuth authentication, transport handling, and integrated deployment.
### LLM Providers Support
Source: [How to use Anthropic MCP Server with open LLMs](https://www.philschmid.de/mcp-example-llama)
MCP is originally designed for Claude but can be used with other LLM by writing custom adapter for it.
**Official Support**:
- OpenAI - [openai-agents-python/mcp/](https://openai.github.io/openai-agents-python/mcp/)
- Microsoft - [MCP in Azure AI Foundry](https://devblogs.microsoft.com/foundry/integrating-azure-ai-agents-mcp/)
**Custom adapters** implementations:
- [MCP: Integrating Azure OpenAI](https://techcommunity.microsoft.com/blog/azure-ai-services-blog/model-context-protocol-mcp-integrating-azure-openai-for-enhanced-tool-integratio/4393788)
	- Github: [mcp_aoai](https://github.com/monuminu/AOAI_Samples/tree/main/mcp_aoai)
- Github: [philschmid/mcp-openai-gemini-llama-example](https://github.com/philschmid/mcp-openai-gemini-llama-example)
- Github: [jalr4ever/Tiny-OAI-MCP-Agent](https://github.com/jalr4ever/Tiny-OAI-MCP-Agent)
- Github: [chrishayuk/mcp-cli](https://github.com/chrishayuk/mcp-cli)