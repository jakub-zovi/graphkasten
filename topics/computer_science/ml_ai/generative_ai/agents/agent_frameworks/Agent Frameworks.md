---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-03-11T18:19
modified: 2026-01-14T13:06
published:
sources:
  - "[Freeing our search agents](https://huggingface.co/blog/open-deep-research)"
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Agent Frameworks
[Freeing our search agents](https://huggingface.co/blog/open-deep-research):
> An Agent framework is a layer on top of an LLM to make said LLM execute actions (like browse the web or read PDF documents), and organize its operations in a series of steps. 
## Resources
- Blogs
	- [Are Agentic Frameworks an Overkill?](https://blog.premai.io/are-agentic-frameworks-an-overkill-benefits-challenges-and-alternatives/)
## List of Frameworks
- [[OpenAI AgentKit]]
	- [Introducing AgentKit](https://openai.com/index/introducing-agentkit/)
	- A visual workflow builder, a connector registry for governance, a drop-in chat UI kit, stronger evals, and reinforcement fine-tuning options. Built to replace fragmented orchestration, manual evals, and ad-hoc frontends with versioned, production-ready components.
- [[autogen]]
	- AutoGen is a framework for creating multi-agent AI applications that can act autonomously or work alongside humans.
	- Github: [microsoft/autogen](https://github.com/microsoft/autogen)
		- **53.5K** stars
- [[agno]]
	- Agno is a lightweight library for building Agents with memory, knowledge, tools and reasoning.
	- Github: [agno-agi/agno](https://github.com/agno-agi/agno)
		- **25.2K** stars
- [[smolagents]]
	- A minimalistic framework by Hugging Face that implements agents using code actions
	- Github: [huggingface/smolagents](https://github.com/huggingface/smolagents)
		- **24.9K** stars
- [[LangGraph]]
	- A framework for defining agentic workflows through graphs by LangChain creators
	- Github: [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph)
		- **10.1K** stars
- [[OpenAI Agents SDK]]
	- A lightweight, easy-to-use package with very few abstractions for building AI apps
	- Github: [openai/openai-agents-python](https://github.com/openai/openai-agents-python)
		- **6.6K** stars
- [[PydanticAI]]
	- An agent framework designed to make it less painful to build production grade applications with Generative AI.
	- Github: [pydantic/pydantic-ai](https://github.com/pydantic/pydantic-ai)
		- **7.3K** stars
- [[NVIDIA AgentIQ]]
	- The core principle of this library is every agent, tool, and agentic workflow exists as a function call - enabling composability between these agents, tools, and workflows.
		- Library additionally provides chatting UI, evaluation system, profiling and much more
	- Github: [NVIDIA/AgentIQ](https://github.com/NVIDIA/AgentIQ)
		- **1.7** stars
- Camel-AI
	- Multi-agent framework focused more on the research? I did not explore this framework.
	- Github: [camel-ai/camel](https://github.com/camel-ai/camel)
		- **10K** stars
## Comparison of Features
Source: [How to think about agent frameworks](https://blog.langchain.dev/how-to-think-about-agent-frameworks/?ref=dailydev)
<img src="https://blog.langchain.dev/content/images/size/w1520/format/webp/2025/04/Screenshot-2025-04-20-at-10.19.41-AM.png" />