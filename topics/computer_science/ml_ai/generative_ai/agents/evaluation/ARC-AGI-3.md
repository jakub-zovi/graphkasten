---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-04-05T00:00
modified: 2026-08-01T11:15
published:
sources:
  - "[ARC-AGI-3: A New Challenge for Frontier Agentic Intelligence](https://arxiv.org/abs/2603.24621)"
topics:
  - Agent Benchmarks
  - Abstract Reasoning
  - Agentic Intelligence
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# ARC-AGI-3
- Part of the ARC-AGI series by the ARC Prize Foundation, focused on evaluating **agentic** (not just predictive) intelligence
- Unlike previous ARC benchmarks, ARC-AGI-3 is **interactive** — agents must act in environments rather than just produce outputs
- Paper: [ARC-AGI-3: A New Challenge for Frontier Agentic Intelligence](https://arxiv.org/abs/2603.24621)
	- Submitted: 2026-03-24
	- Authors: ARC Prize Foundation

## Abstract
> Agents must explore, infer goals, build internal models of environment dynamics, and plan effective action sequences without explicit instructions.

## Key Points
- **Interactive benchmark** — agents explore dynamic environments, infer goals, and plan actions without being given explicit instructions
- **No language or external knowledge required** — grounded purely in Core Knowledge priors to avoid memorization shortcuts
- **Human-calibrated difficulty** — environments validated through extensive human testing with established human performance baselines
- **Scoring by efficiency** — success is measured relative to human action baselines, not just binary task completion

## Results (as of 2026-03-24)
- Human test-takers: **100% success rate**
- Frontier AI systems: **<1% score**
- Represents a stark gap between human and AI adaptive problem-solving on novel tasks

## Why It Matters
- Previous benchmarks (including ARC-AGI-1 and ARC-AGI-2) were largely solved or approached by frontier models through pattern matching and memorization
- ARC-AGI-3 forces genuine exploration and goal inference — capabilities that current LLMs fundamentally lack
- Sets a new milestone target for the field: matching human efficiency on novel interactive tasks
