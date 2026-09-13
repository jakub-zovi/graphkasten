---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-03-13T10:46
modified: 2026-01-15T11:27
published:
sources:
  - "[Introducing smolagents](https://huggingface.co/blog/smolagents)"
topics:
  - smolagents
authors:
ai-assisted:
hidden:
public: true
---
# Code Actions
In a multi-step agent, at each step, the LLM can write an action, in the form of some calls to external tools. A common format for writing these actions is generally different shades of writing actions as a JSON. **But research have shown that having the tool calling LLMs in code is much better.** The reason for this is simply that we crafted our code languages specifically to be the best possible way to express actions performed by a computer ([Source](https://huggingface.co/blog/smolagents#code-agents)).

Advantages of using code actions ([Figure Source](https://arxiv.org/abs/2402.01030)):
<img src="https://i-blog.csdnimg.cn/blog_migrate/4c4ad35ac334925821d2f44b9dc5dc39.png">
## Papers
- [Executable Code Actions Elicit Better LLM Agents](https://arxiv.org/abs/2402.01030)
	- This work proposes to use executable Python code to consolidate LLM agents' actions into a unified action space (CodeAct). Integrated with a Python interpreter, CodeAct can execute code actions and dynamically revise prior actions or emit new actions upon new observations through multi-turn interactions.
	- 144 citations
	- Submitted on 1 Feb 2024
- [If LLM Is the Wizard, Then Code Is the Wand](https://arxiv.org/abs/2401.00812)
	-  Enhancing LLMs in code generation, we observe that these unique properties of code help (i) unlock the reasoning ability of LLMs, enabling their applications to a range of more complex natural language tasks; (ii) steer LLMs to produce structured and precise intermediate steps, which can then be connected to external execution ends through function calls; and (iii) take advantage of code compilation and execution environment, which also provides diverse feedback for model improvement.
	- 69 citations
	- Submitted on 1 Jan 2024
- [DynaSaur: Large Language Agents Beyond Predefined Actions](https://arxiv.org/abs/2411.01747)
	- Proposes an LLM agent framework that enables the dynamic creation and composition of actions in an online manner. In this framework, the agent interacts with the environment by generating and executing programs written in a general-purpose programming language at each step. Furthermore, generated actions are accumulated over time for future reuse.
	- 5 citations
	- Submitted on 4 Nov 2024