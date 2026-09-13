---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-05-20T12:00
modified: 2026-08-01T11:10
published:
sources:
  - "[AI Memory Benchmarks in 2026 - Mem0](https://mem0.ai/blog/ai-memory-benchmarks-in-2026)"
  - "[Hindsight Is #1 on BEAM](https://hindsight.vectorize.io/blog/2026/04/02/beam-sota)"
  - "[Agent Memory Benchmark](https://agentmemorybenchmark.ai/)"
topics:
  - Agent Memory
  - Long-Term Memory Evaluation
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
---
# Agent Memory Benchmarks
- A memory benchmark gives a system a sequence of inputs over time, requires the system to write something to a store, and asks the system to retrieve from that store on a later turn to produce the right answer ([AI Memory Benchmarks in 2026](https://mem0.ai/blog/ai-memory-benchmarks-in-2026)).
- Distinct from LLM Benchmarks(NIAH, RULER, BABILong, InfiniteBench, LongBench) that test attention over a single fixed input rather than the multi-session write-and-retrieve loop.
> Capacity and continuity are different problems. The same score does not measure both.
## List Of Benchmarks

| Benchmark        | Year       | What it adds                                       |
| ---------------- | ---------- | -------------------------------------------------- |
| [[LoCoMo]]       | 2024       | Very long multi-session dialogue at scale          |
| [[LongMemEval]]  | 2024       | Five abilities, including knowledge updates and abstention |
| [[BEAM]]         | 2026 (ICLR)| Ten memory capabilities up to 10M tokens           |

- [[LoCoMo]]
	- Very long-term conversational memory benchmark - ~300 turns and ~9,000 tokens spread across up to 35 sessions per conversation
	- Paper: [Evaluating Very Long-Term Conversational Memory of LLM Agents](https://arxiv.org/abs/2402.17753)
		- 2024
		- Maharana, Lee, Tulyakov, Bansal, Barbieri, Fang
- [[LongMemEval]]
	- Chat-assistant memory benchmark with 500 curated questions, five abilities: information extraction, multi-session reasoning, temporal reasoning, knowledge updates, abstention
	- Two splits: `LongMemEval_S` (~115K tokens, ~40 sessions/user) and `LongMemEval_M` (~500 sessions/user)
	- Paper: [LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory](https://arxiv.org/abs/2410.10813)
		- 2024
		- Wu, Wang, Yu, Zhang, Chang, Yu
- [[BEAM]]
	- 100 conversations spanning up to 10M tokens with 2,000 probing questions; tests ten memory capabilities including tracking facts/entities, updating information, resolving contradictions, temporal order, multi-hop reasoning, summarization
	- Two tracks: BEAM-1M and BEAM-10M
	- Paper: [Beyond a Million Tokens: Benchmarking and Enhancing Long-Term Memory in LLMs](https://arxiv.org/pdf/2510.27246)
		- Submitted 2025-10-31, ICLR 2026
		- Tavakoli, Salemi, Ye, Abdalla, Zamani, Mitchell
	- Github: [mohammadtavakoli78/BEAM](https://github.com/mohammadtavakoli78/BEAM)
	- Dataset: [Mohammadta/BEAM on HuggingFace](https://huggingface.co/datasets/Mohammadta/BEAM)
	- Companion framework: LIGHT - three complementary memory systems (long-term episodic, short-term working, scratchpad). Reports 3.5-12.7% accuracy improvement over strongest long-context baselines
## Leaderboards & Trackers
- [Agent Memory Benchmark](https://agentmemorybenchmark.ai/)
	- Public leaderboard tracking BEAM and related benchmarks across memory systems
	- [BEAM leaderboard](https://agentmemorybenchmark.ai/dataset/beam)
## Current Gaps
- **Cross-session continuity at production scale** - LoCoMo tops at ~35 sessions, LongMemEval_M at ~500, BEAM at 10M tokens; no stable definition of "long enough" for year-long personal assistants
- **Memory writes** - almost every public benchmark grades only retrieval, not what is worth keeping
- **Forgetting, eviction, consolidation** - no widely adopted benchmark scores these dynamics directly; BEAM's contradiction/update subscores get closest
- **Per-user isolation** - none of the public benchmarks test isolation under concurrent multi-user load
- **Token economy under realistic budgets** - leaderboards usually ignore tokens-per-query cost
## Resources
- Blogs
	- [[AI Memory Benchmarks in 2026]] ([Link](https://mem0.ai/blog/ai-memory-benchmarks-in-2026))
		- [Original article on mem0.ai](https://mem0.ai/blog/ai-memory-benchmarks-in-2026)
		- 2026-05-11
		- Walkthrough of LoCoMo, LongMemEval, BEAM and where evals fall short
	- [[Hindsight Is 1 on BEAM — the Benchmark That Tests Memory at 10 Million Tokens|Hindsight Is #1 on BEAM]] ([Link](https://hindsight.vectorize.io/blog/2026/04/02/beam-sota))
		- [Original article on vectorize.io](https://hindsight.vectorize.io/blog/2026/04/02/beam-sota)
		- 2026-04-02
		- SOTA result on BEAM-10M and discussion of why the 10M tier matters
	- [[The Memory Layer for your AI Agents]] ([Link](https://mem0.ai/blog/what-is-beam-memory-benchmark-the-paper-that-shows-1m-context-window-isnt-enough))
		- [Original article on mem0.ai](https://mem0.ai/blog/what-is-beam-memory-benchmark-the-paper-that-shows-1m-context-window-isnt-enough)
		- 2026-04-02
		- Mem0's explainer on BEAM — generation pipeline, ten memory capabilities, LIGHT framework results, and nugget-based evaluation
- Papers
	- [Beyond a Million Tokens: Benchmarking and Enhancing Long-Term Memory in LLMs](https://arxiv.org/pdf/2510.27246)
		- 2025-10-31 (ICLR 2026)
