---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-11-16T10:14
modified: 2025-11-16T10:16
published:
sources:
  - "[AI Agents Weekly](https://nlp.elvissaravia.com/p/ai-agents-weekly-omnilingual-asr?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa7a672e4-d08b-4012-a8ff-fb9c86e1fbc3_2268x1404.png&open=false)"
  - "[The Era of Agentic Organization: Learning to Organize with Language Models](https://arxiv.org/pdf/2510.26658)"
topics:
authors:
ai-assisted:
hidden:
public: true
---
# The Era of Agentic Organization
![](https://substackcdn.com/image/fetch/$s_!7ru7!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa7a672e4-d08b-4012-a8ff-fb9c86e1fbc3_2268x1404.png)

Microsoft Research introduces AsyncThink (Asynchronous Thinking), a breakthrough reasoning paradigm where LLMs learn to organize their internal thinking into concurrently executable structures through an organizer-worker protocol. Moving beyond sequential and parallel thinking, AsyncThink enables agents to collaboratively solve complex problems by dynamically decomposing tasks and executing sub-queries concurrently.

- **Organizer-worker thinking protocol:** An organizer dynamically assigns sub-queries to workers using Fork and Join actions. The entire protocol operates through pure text generation, making it compatible with existing LLMs without architectural changes.
    
- **Learning to organize through RL:** Two-stage training with cold-start format fine-tuning followed by reinforcement learning using Group Relative Policy Optimization. Rewards encourage correctness, format compliance, and thinking concurrency.
    
- **Superior accuracy-latency frontier:** AsyncThink achieves 28% lower inference latency compared to parallel thinking while improving accuracy on mathematical reasoning. On AIME-24, it matches parallel thinking’s 38.7% accuracy with 1,468 latency versus 2,048.
    
- **Remarkable generalization:** Models trained solely on multi-solution countdown tasks demonstrate zero-shot asynchronous thinking on previously unseen domains, including Sudoku, graph theory, and genetics problems.
    
- **Scalability pathways:** Future directions include massive agent pools with heterogeneous expert workers, recursive agentic organization where workers can become sub-organizers, and human-AI collaborative frameworks.