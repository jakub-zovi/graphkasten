---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-11-16T10:07
modified: 2026-07-21T09:02
published:
sources:
topics:
  - Design Patterns
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Agentic Design
This note aggregates information about how to design agents and best practices when implementing them.
## Approaches
- [[Agent Skills]]
- [[Agent Harness]]
- [[Structured Output]]
- [[Tool Calling]]
## Resources
- [[Toward Efficient Agents - Memory, Tool learning, and Planning]]
- [m-ric Collections Agents](https://huggingface.co/collections/m-ric/agents-65ba776fbd9e29f771c07d4e) - collection of academic papers about agents
- [[The Era of Agentic Organization]]
	- Research By Microsoft
	- 2025-11-15
- [[Agents Best Practices]]
	- Anthropic
	- 2024-12-09
- [[Structuring Agents, Skills, and MCPs Best Practices from Anthropic]] ([Link](https://medium.com/intuitionmachine/structuring-agents-skills-and-mcps-best-practices-from-anthropic-9312849ccea6))
	- Carlos E. Perez
	- 2026-05-06 — three-layer architecture (skills / agents / MCP) derived from Anthropic's finance-agents reference
- [[Towards a science of scaling agent systems When and why agent systems work]] ([Link](https://research.google/blog/towards-a-science-of-scaling-agent-systems-when-and-why-agent-systems-work/))
	- Google Research
	- 2026-01-28 — controlled evaluation of 180 agent configurations across 5 canonical architectures (single-agent, independent, centralized, decentralized, hybrid); multi-agent helps on parallelizable tasks but degrades sequential ones