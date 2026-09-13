---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-03-13T15:20
modified: 2025-11-08T18:12
published:
sources:
  - "[Anthropic - Building effective agents](https://www.anthropic.com/engineering/building-effective-agents), [Building good agents](https://huggingface.co/docs/smolagents/tutorials/building_good_agents#building-good-agents)"
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Agents Best Practices
There are many aspects to take into consideration when developing AI agent. In this page, I try to summarize tips and tricks from the sources specified above. Additionally, I also include some of my personal insights in developing these systems.
## Minimize LLM use
Each use of a LLM introduces uncertainty and risk into the system. Therefore, LLM usage should be kept at a minimum. Furthermore, go through this checklist when deciding whether to employ LLM for a given component of the system:
1. Can it be implemented with **software engineering**? 
2. Can it be achieved with **traditional machine learning**? 
3. If answer to both questions above is no, then use a **LLM**.
## Agentic Frameworks
Only employ a framework when you **understand underlying abstraction** that it implements. Otherwise, the solution can become hard to debug and modify. Ideally, try to implement as many parts of the solution as possible without framework ([Anthropic - Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)). 
## Improve the information flow
 [Building good agents](https://huggingface.co/docs/smolagents/tutorials/building_good_agents#building-good-agents):
> **Make your task very clear!** Since an agent is powered by an LLM, minor variations in your task formulation might yield completely different results.
> Then, improve the information flow towards your agent in tool use.
> 
> Particular guidelines to follow:
> - Each tool should log (by simply using print statements inside the tool’s forward method) everything that could be useful for the LLM engine.
> 	- In particular, logging detail on tool execution errors would help a lot!

