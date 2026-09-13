---
tags:
  - gen_ai
  - gen_ai/agents
created: 2026-08-05T10:00
modified: 2026-08-05T10:00
published: 2025-04-16
sources:
  - "[BrowseComp: A Simple Yet Challenging Benchmark for Browsing Agents](https://arxiv.org/pdf/2504.12516)"
topics:
  - Agent Benchmarks
  - Web Browsing Agents
  - Deep Research
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
---
# BrowseComp
- OpenAI benchmark for evaluating browsing agents on hard information-retrieval tasks that need persistence and creativity across many web pages
- Paper: [BrowseComp: A Simple Yet Challenging Benchmark for Browsing Agents](https://arxiv.org/pdf/2504.12516)
	- Submitted on 2025-04-16
	- Authors: Jason Wei, Zhiqing Sun, Spencer Papay, Scott McKinney, Jeffrey Han, Isa Fulford, Hyung Won Chung, Alex Tachard Passos, William Fedus, Amelia Glaese
- Blog: [[Introducing BrowseComp (Blog)]]

## Abstract
> We present BrowseComp, a simple yet challenging benchmark for measuring the ability of agents to browse the web. BrowseComp comprises 1,266 questions that require persistently navigating the internet in search of hard-to-find, entangled information. Despite the difficulty of the questions, BrowseComp is simple and easy to use, as predicted answers are short and easily verifiable against reference answers. BrowseComp for browsing agents can be seen as analogous to how programming competitions are an incomplete but useful benchmark for coding agents.

## Benchmark Specs
- **1,266 questions** — each has a short, verifiable ground-truth answer
- Questions built by **inverse construction**: trainer starts from a rare fact, then adds constraints until the target becomes unique and hard to Google directly
- Answer format kept short (name, date, number) so grading is deterministic — reduces LLM-judge noise
- Trainers themselves could not solve most items in under two hours of browsing — establishes the difficulty floor

## Scoring
- **Accuracy** — exact-match against reference answer, verified by LLM grader
- **Calibration** — models also emit a confidence; paper reports Brier-style calibration curves

## Headline Results
- Humans (trainers, 2h cap): solve **~30%** of questions
- GPT-4o (no browsing): **~1%**
- GPT-4o + browsing tool: **~2%**
- OpenAI **Deep Research**: **~52%** — best of the tested systems
- Test-time compute scaling (best-of-N + aggregation) gives large lifts over single-shot browsing

## Why It Matters
- Isolates the "find the needle" capability that generic web QA benchmarks (SimpleQA, TriviaQA) do not stress — most facts here need multi-hop cross-referencing across obscure sources
- Short verifiable answers sidestep the judge-quality problem that plagues open-ended agent benchmarks
- Became the reference eval for browsing / deep-research agents released after 2025-Q2
