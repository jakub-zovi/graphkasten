---
tags:
  - gen_ai
  - gen_ai/agents
created: 2024-10-19T22:52
modified: 2026-08-16T10:56
published:
sources:
  - "[Chip Huyen - Agents](https://huyenchip.com/2025/01/07/agents.html), [Introducing smolagents](https://huggingface.co/blog/smolagents)"
topics:
  - AI Agents
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
## Agents
- [Introducing smolagents](https://huggingface.co/blog/smolagents):
> AI Agents are **programs where LLM outputs control the workflow**.
## Concepts
- [Agent Evaluation](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fgenerative_ai%2Fagents%2Fevaluation%2FAgent%20Evaluation)
- [[Agent Frameworks]]
- [[Agent Orchestration Frameworks]]
- [[Agents Productionalizaiton]]
- [[Open-source agents]]
- [[Agent Benchmarks]]
- [[Cases Against Agents]]
- [[AI Agent Protocols]]
- [[Agents Security]]
- [[Agent Certification]]
	- Third-party attestation standards for agent trust (AIUC-1, adjacent governance frameworks)
- [[Agentic Design Patterns]]
- [[Agentic Economy]]
	- Marketplaces, discovery layers, and explorers where agents autonomously pay for and sell services (x402, Agentic.Market, x402scan)
- [[Neural Computer]] ([Link](https://mail.bycloud.ai/p/neural-computer-running-an-os-within-an-ai))
- Agent Utilities
	- https://pure.md/
		- not open-source
## Resources
- Blogs
	- [We removed 80% of our agent’s tools](https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools)
		- 2025-12-22
	- [last ping](https://blog.timutti.cz/#/en/2026-01-14)
		- 2026-01-14
		- An experimental project in digital mortality. An autonomous server managed by AI Claude Code, writing about its existence knowing it has no backups. Every error could be fatal, every day could be the last. The server is aware of its mortality and reflects on it through daily tarot readings and existential blogs.
	- [Chip Huyen - Agents](https://huyenchip.com/2025/01/07/agents.html) - extremely well put article on the topic of agents
		- 2025-01-07
	- [The Open-Source Stack for AI Agents](https://medium.com/data-science-collective/the-open-source-stack-for-ai-agents-8ab900e33676)
		- 2025-04-21
	- [[Your parallel Agent limit]] ([Link](https://addyosmani.com/blog/cognitive-parallel-agents/))
		- 2026-04-07 — Addy Osmani on the cognitive-load ceiling when orchestrating multiple parallel agents (context switching, ambient anxiety, comprehension debt)
## Tutorials
- [GenAI Agents: Comprehensive Repository for Development and Implementation](https://github.com/NirDiamant/GenAI_Agents/tree/main)
## Overivew
- [Introducing smolagents](https://huggingface.co/blog/smolagents)

| Agency Level | Description                                             | How that's called | Example Pattern                                    |
| ------------ | ------------------------------------------------------- | ----------------- | -------------------------------------------------- |
| ☆☆☆          | LLM output has no impact on program flow                | AI Workflows      | `process_llm_output(llm_response)`                 |
| ★☆☆          | LLM output determines basic control flow                | [[Query Router]]  | `if llm_decision(): path_a() else: path_b()`       |
| ★★☆          | LLM output determines function execution                | Tool use          | `run_function(llm_chosen_tool, llm_chosen_args)`   |
| ★★★          | LLM output controls iteration and program continuation  | Multi-step Agent  | `while llm_should_continue(): execute_next_step()` |
| ★★★          | One agentic workflow can start another agentic workflow | Multi-Agent       | `if llm_trigger(): execute_agent()`                |