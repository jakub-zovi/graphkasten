---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-05-23T10:00
modified: 2026-08-01T11:16
published: 2024-07-26
sources:
  - "[AppWorld: A Controllable World of Apps and People for Benchmarking Interactive Coding Agents](https://arxiv.org/pdf/2407.18901)"
  - "[AppWorld Leaderboard](https://appworld.dev/leaderboard)"
topics:
  - Agent Benchmarks
  - Tool Use
  - Interactive Coding
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
---
# AppWorld
- A controllable simulation environment for benchmarking autonomous agents on **interactive coding** tasks across realistic day-to-day apps
- Awarded **ACL 2024 Best Resource Paper**
- Paper: [AppWorld: A Controllable World of Apps and People for Benchmarking Interactive Coding Agents](https://arxiv.org/pdf/2407.18901)
	- 210 citations
	- Submitted on 2024-07-26
	- Authors: Harsh Trivedi, Tushar Khot, Mareike Hartmann, Ruskin Manku, Vinty Dong, Edward Li, Shashank Gupta, Ashish Sabharwal, Niranjan Balasubramanian
- Github: [StonyBrookNLP/appworld](https://github.com/StonyBrookNLP/appworld)
	- 423 stars
- Project site: [appworld.dev](https://appworld.dev/) — includes task explorer, API explorer, and the public [leaderboard](https://appworld.dev/leaderboard)

## Abstract
> Autonomous agents that address day-to-day digital tasks (e.g., ordering groceries for a household), must not only operate multiple apps (e.g., notes, messaging, shopping app) via APIs, but also generate rich code with complex control flow in an iterative manner based on their interaction with the environment. To facilitate the development of such agents, we build AppWorld Engine, a high-quality execution environment (60K lines of code) of 9 day-to-day apps operable via 457 APIs and populated with realistic digital activities simulating the lives of ~100 fictitious users. We then create AppWorld Benchmark (40K lines of code), a suite of 750 natural, diverse, and challenging autonomous agent tasks requiring rich and interactive code generation.

## Benchmark Specs
- **9 apps** — modelled after real-world services (Amazon, Spotify, Venmo, SimpleNote, Gmail, etc.)
- **457 APIs** across the apps
- **~100 simulated users** populating the environment with realistic digital activity
- **750 tasks** split into `Test-Normal` and `Test-Challenge` difficulty tiers
- **State-based unit tests** as the evaluation mechanism — checks final environment state and detects unintended side effects ("collateral damage")

## Scoring Metrics
- **TGC** — *Task Goal Completion*: whether the full task goal was achieved
- **SGC** — *Scenario Goal Completion*: completion at the scenario level (subgoals satisfied)
- Reported across difficulty **Level 1 / Level 2 / Level 3** and both Test-Normal and Test-Challenge splits

## Headline Results
- Original paper (2024): GPT-4o reaches ~49% on Test-Normal and ~30% on Test-Challenge; all other tested models trail by at least 16 points
- Current SOTA (per [leaderboard](https://appworld.dev/leaderboard)): **CUGA** ([Towards Enterprise-Ready Computer Using Generalist Agent](https://arxiv.org/pdf/2503.01861)) — >91% TGC on Level 1, drops to ~38% on Level 3
- RL-trained agents (Qwen2.5-32B-Instruct + LOOP) reach ~71% TGC, beating OpenAI o1 by ~9 points (15% relative)

## Why It Matters
- Goes beyond static QA or single-tool benchmarks: agents must write **multi-step interactive code** that calls APIs, branches on results, and recovers from errors
- State-based evaluation catches agents that "succeed" while corrupting unrelated state — closer to how real assistants would be judged in production
- Used as a reference benchmark in subsequent agent papers (e.g. CUGA, LOOP RL training) for measuring tool-use and coding-agent capability
