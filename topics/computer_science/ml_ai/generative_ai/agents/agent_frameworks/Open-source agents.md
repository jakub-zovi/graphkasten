---
tags:
  - gen_ai
  - gen_ai/agents
created: 2024-11-10T17:52
modified: 2026-03-28T13:50
published:
sources:
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Open-source Agents
- [[AlphaEvolve]]: A coding agent for scientific and algorithmic discovery
	-  LLMs have shown promise in accelerating scientific discovery, but their ability to generate entirely novel, high-impact algorithms has been limited. This is mainly because they rely on static training data and can not refine their solutions. AlphaEvolve fixes this by creating a dynamic feedback loop where code is written, tested, criticized, and improved autonomously.
	- Paper: [AlphaEvolve: A Gemini-powered coding agent for designing advanced algorithms](https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/?ref=mail.bycloud.ai)
	- by_cloud blog: [The AI Timeline: AlphaEvolve](https://mail.bycloud.ai/p/alphaevolve)
- [[Voyager]]
	- Voyager, the first LLM-powered embodied lifelong learning agent in Minecraft that continuously explores the world, acquires diverse skills, and makes novel discoveries without human intervention. Voyager consists of three key components: 1) an automatic curriculum that maximizes exploration, 2) an ever-growing skill library of executable code for storing and retrieving complex behaviors, and 3) a new iterative prompting mechanism that incorporates environment feedback, execution errors, and self-verification for program improvement.
	- Implementation: [MineDojo/Voyager](https://github.com/MineDojo/Voyager)
		- **6.1k** stars
	- [Paper: Voyager: An Open-Ended Embodied Agent](https://voyager.minedojo.org/)
		- 1000 citations
		- 2023-10-19
- [[SWE-agent]]
	- A system that facilitates LM agents to autonomously use computers to solve software engineering tasks. SWE-agent's custom agent-computer interface (ACI) significantly enhances an agent's ability to create and edit code files, navigate entire repositories, and execute tests and other programs
	- Implementation: https://github.com/princeton-nlp/SWE-agent
	- Paper: [SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering](https://arxiv.org/abs/2405.15793)
		- 164 citations
		- Submitted on 6 May 2024
	- [Youtube Presentation](https://www.youtube.com/watch?v=d9gcXpiiDao&ab_channel=Weights%26Biases)
- [[Magentic-One]]
	- A high-performing generalist agentic system designed to solve such tasks. Magentic-One employs a multi-agent architecture where a lead agent, the Orchestrator, directs four other agents to solve tasks. The Orchestrator plans, tracks progress, and re-plans to recover from errors, while directing specialized agents to perform tasks like operating a web browser, navigating local files, or writing and executing Python code.
	- Implementation: https://github.com/microsoft/autogen/tree/v0.4.4/python/packages/autogen-magentic-one
	- Blog:  [AI Frontiers blog](https://www.microsoft.com/en-us/research/articles/magentic-one-a-generalist-multi-agent-system-for-solving-complex-tasks/)
	- Paper: [Magentic-One: A Generalist Multi-Agent System for Solving Complex Tasks](https://arxiv.org/abs/2411.04468)
		- 15 citations
		- Submitted on 7 Nov 2024
- [[Open Deep Search]]
	- Open-source replication of the [OpenAI deep research](https://openai.com/index/introducing-deep-research/) agent by HuggingFace with the use of of smolagents library
	- Implementation: https://github.com/huggingface/smolagents/tree/main/examples/open_deep_research
	- Blog: [Open-source DeepResearch – Freeing our search agents](https://huggingface.co/blog/open-deep-research)
- Other agents reproducing [OpenAI deep research](https://openai.com/index/introducing-deep-research/):
	- [dzhng/deep-research](https://github.com/dzhng/deep-research)
	- [assafelovic/gpt-researcher](https://github.com/assafelovic/gpt-researcher)