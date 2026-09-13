---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-04-04T10:00
modified: 2026-08-01T11:11
published:
sources:
  - "[Agentic Web: Weaving the Next Web with AI Agents](https://arxiv.org/abs/2507.21206)"
topics:
  - Agentic Web
  - Multi-Agent Systems
  - Agent Communication Protocols
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Agentic Web
- [Agentic Web: Weaving the Next Web with AI Agents](https://arxiv.org/abs/2507.21206)
> The emergence of AI agents powered by large language models (LLMs) marks a pivotal shift toward the Agentic Web, a new phase of the internet defined by autonomous, goal-driven interactions.

- The web is evolving from human-driven interaction to machine-to-machine interaction where agents plan, coordinate, and execute complex tasks autonomously
- The paper proposes a structured framework built around three key dimensions: **intelligence**, **interaction**, and **economics**

## Core Framework
- **Intelligence** — the cognitive layer of individual agents
	- Retrieval: accessing and synthesising web-scale information
	- Recommendation: personalised, context-aware suggestions
	- Planning: decomposing goals into executable sub-tasks
	- Collaboration: coordinating with other agents or humans
- **Interaction** — how agents communicate and coordinate
	- Communication protocols between agents (see AI Communication Protocols)
	- Orchestration strategies for multi-agent pipelines (see [Agentic Design Patterns](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fgenerative_ai%2Fagents%2Fdesign%2FAgentic%20Design%20Patterns))
	- Tool and API integration with existing web infrastructure
- **Economics** — incentive structures governing agent behaviour
	- **Agent Attention Economy**: agents competing for computational resources, API bandwidth, and user attention in a market-like fashion
	- Economic incentives for cooperation vs. competition among agents
	- Micropayment and value-exchange primitives for autonomous transactions (see Payment Protocols)

## Architectural Challenges
- Communication protocols — standardising how agents expose capabilities and exchange messages (see AI Communication Protocols)
- Orchestration — managing task delegation, context passing, and failure recovery across agent networks
- Scalability — maintaining coherent behaviour as agent networks grow
- Integration — fitting autonomous agents into existing HTTP/web service infrastructure without breaking backward compatibility

## Agent Attention Economy
- Concept introduced by the paper to describe resource allocation in multi-agent environments
- Agents must compete or negotiate for: API rate limits, LLM inference slots, human oversight bandwidth
- Creates emergent market dynamics analogous to advertising auctions on today's web
- Raises questions about fairness, monopolisation, and optimal mechanism design

## Applications
- Web automation — end-to-end task execution across browser-accessible services
- Information retrieval & synthesis — multi-hop research across live web sources
- Scientific research assistance — hypothesis generation, literature review, experiment design
- Data analysis pipelines — agents chaining retrieval, computation, and reporting
- Autonomous commerce — price negotiation, procurement, fulfilment

## Resources
- Paper
	- [Agentic Web: Weaving the Next Web with AI Agents](https://arxiv.org/abs/2507.21206)
		- 17 authors incl. Pieter Abbeel, Dawn Song, Weinan Zhang, Jun Wang
		- 2025-07-28
		- arXiv: cs.AI, cs.LG
