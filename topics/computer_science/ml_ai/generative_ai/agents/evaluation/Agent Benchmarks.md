---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-03-12T16:18
modified: 2026-08-21T15:46
published:
sources:
topics:
  - Agent Benchmark
authors:
  - Jakub
ai-assisted: false
hidden:
public: true
---
# Agent Benchmarks
This page aggregates benchmarks specifically designed for evaluating agents based on the LLMs. It differs from LLM Benchmarks page which focuses on benchmarks designed specifically for LLMs, even though there might be some overlap between these benchmarks.
## Sub-Hubs
- [[Agent Memory Benchmarks]]
	- LoCoMo, LongMemEval, BEAM - multi-session memory evaluation distinct from long-context attention
- [[Mercor Benchmarks]]
	- Mercor Research's APEX family — cross-domain, SWE, agents, accounting
## List of Benchmarks
- [[ARC-AGI-3]]
	- Interactive agentic benchmark requiring goal inference, environment modeling, and action planning without explicit instructions; frontier AI scores <1% vs 100% human
	- Paper: [ARC-AGI-3: A New Challenge for Frontier Agentic Intelligence](https://arxiv.org/abs/2603.24621)
		- Submitted on 2026-03-24
- [[A Benchmark for Conversational Data Retrieval]]
- [[WebArena]]
	- Agentic benchmark based on operating in a web environment
	- Paper: [WebArena: A Realistic Web Environment for Building Autonomous Agents](https://arxiv.org/abs/2307.13854)
		- 317 citations
		- Submitted on 2023-7-25
- [[AgentBench]]
	-  A multi-dimensional evolving benchmark that currently consists of 8 distinct environments to assess LLM-as-Agent's reasoning and decision-making abilities in a multi-turn open-ended generation setting
	- Paper: [AgentBench: Evaluating LLMs as Agents](https://arxiv.org/abs/2308.03688)
		- 146 citations
		- Submitted on 7 Aug 2023
- [[GAIA2]]
	- We introduce Gaia2, a benchmark for evaluating large language model agents in realistic, asynchronous environments. Unlike prior static or synchronous evaluations, Gaia2 introduces scenarios where environments evolve independently of agent actions, requiring agents to operate under temporal constraints, adapt to noisy and dynamic events, resolve ambiguity, and collaborate with other agents.
	- Paper: [GAIA2: BENCHMARKING LLM AGENTS ON DYNAMIC AND ASYNCHRONOUS ENVIRONMENTS](https://arxiv.org/pdf/2602.11964)
		- 2026-02-12
		- 7 citations
- [[GAIA]]
	- A benchmark for General AI Assistants that, if solved, would represent a milestone in AI research. GAIA proposes real-world questions that require a set of fundamental abilities such as reasoning, multi-modality handling, web browsing, and generally tool-use proficiency.
	- [Public Leaderboard](https://huggingface.co/spaces/gaia-benchmark/leaderboard)
	- Paper: [GAIA: a benchmark for General AI Assistants](https://arxiv.org/abs/2311.12983)
		- 100 citations
		- Submitted on 21 Nov 2023
- [[τ2-bench]]
	- Paper: [τ2 -Bench: Evaluating Conversational Agents in a Dual-Control Environment](https://arxiv.org/pdf/2506.07982)
		- 93 citations
		- Submitted on 9 Jun 2025
- [[τ-bench]]
	- A benchmark emulating dynamic conversations between a user (simulated by language models) and a language agent provided with domain-specific API tools and policy guidelines
	- Paper: [τ-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains](https://arxiv.org/abs/2406.12045)
		- 20 citations
		- Submitted on 17 Jun 2024
- [[AppWorld]]
	- Controllable simulation of 9 day-to-day apps (457 APIs, ~100 simulated users) with 750 interactive coding tasks; ACL'24 Best Resource Paper
	- Paper: [AppWorld: A Controllable World of Apps and People for Benchmarking Interactive Coding Agents](https://arxiv.org/pdf/2407.18901)
		- 210 citations
		- Submitted on 2024-07-26
- [[BrowseComp]]
	- 1,266 hard-to-Google questions with short verifiable answers; OpenAI benchmark for browsing / deep-research agents. Humans ~30%, Deep Research ~52%
	- Paper: [BrowseComp: A Simple Yet Challenging Benchmark for Browsing Agents](https://arxiv.org/pdf/2504.12516)
		- Submitted on 2025-04-16