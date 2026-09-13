---
tags:
  - cs
  - cs/swe
created: 2026-04-04T12:00
modified: 2026-07-26T13:47
published:
sources:
  - "[Composer 2 Technical Report](https://arxiv.org/abs/2603.24477)"
topics:
  - Agentic Software Engineering
  - Model Training
  - Benchmarks
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Composer 2
- Specialized model by [[Cursor]] Research for **agentic software engineering**
- Focus: long-term planning and coding intelligence in multi-step, realistic dev environments
- 54 authors; March 25, 2026
- Paper: [Composer 2 Technical Report](https://arxiv.org/abs/2603.24477)

## Training
- Two-phase approach:
	- **Continued pretraining** on code and software engineering data
	- **Large-scale reinforcement learning** on realistic coding problems
- Training infrastructure mirrors the actual Cursor deployment harness — same tools, environments, and structure used in production

## Benchmarks
| Benchmark | Score |
|---|---|
| CursorBench | 61.3 |
| Terminal-Bench | 61.7 |
| SWE-bench Multilingual | 73.7 |

- **CursorBench** — internal benchmark derived from real software engineering challenges faced by Cursor users; measures practical agentic coding ability
- **Terminal-Bench** — evaluates terminal-based software engineering tasks
- **SWE-bench Multilingual** — real GitHub issues across multiple programming languages

## Key Ideas
- Training on environments that closely match real problems (not toy tasks) is central to the model's effectiveness
- RL with execution feedback allows the model to learn from actual code running — not just human labels
- Significant improvement over prior Composer versions on all benchmarks
