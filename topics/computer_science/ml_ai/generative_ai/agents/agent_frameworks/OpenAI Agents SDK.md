---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-03-19T18:00
modified: 2025-11-08T18:12
published:
sources:
  - "[OpenAI Agents SDK](https://openai.github.io/openai-agents-python/), [openai/openai-agents-python](https://github.com/openai/openai-agents-python)"
topics:
authors:
ai-assisted:
hidden:
public: true
---
# OpenAI Agents SDK
[OpenAI Agents SDK](https://openai.github.io/openai-agents-python/):
The OpenAI Agents SDK enables you to build agentic AI apps in a lightweight, easy-to-use package with very few abstractions. It's a production-ready upgrade of our previous experimentation for agents, Swarm. The Agents SDK has a very small set of primitives:
- Agents, which are LLMs equipped with instructions and tools
- Handoffs, which allow agents to delegate to other agents for specific tasks
- Guardrails, which enable the inputs to agents to be validated
## Core Concepts
 [openai/openai-agents-python](https://github.com/openai/openai-agents-python):
- Agents: LLMs configured with instructions, tools, guardrails, and handoffs
- Handoffs: A specialized tool call used by the Agents SDK for transferring control between agents
- Guardrails: Configurable safety checks for input and output validation
- Tracing: Built-in tracking of agent runs, allowing you to view, debug and optimize your workflows