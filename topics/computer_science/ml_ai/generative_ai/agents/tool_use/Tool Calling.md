---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-02-03T17:14
modified: 2026-07-21T09:04
published:
sources:
  - "[Prompting Techniques - Automatic Reasoning and Tool-use](https://www.promptingguide.ai/techniques/art)"
topics:
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Tool Calling
- Modern LLMs are able to identify the need for usage of external tools such as calculators. Process of tool selection is different from Model Routing since the LLM needs to determined how the tool should be used. Also, LLMs are capable of selecting and evaluating tools in one go with ART framework (see below). [[Function Calling]] can be considered only a different name to the tool use.
## Resources
- Papers
	- [HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face](https://proceedings.neurips.cc/paper_files/paper/2023/file/77c33e6a367922d003ff102ffb92b658-Paper-Conference.pdf)
		- 1037 citations
	- [ART: Automatic multi-step reasoning and tool-use for large language models](https://arxiv.org/abs/2303.09014)
		- 197 citaitons
	- [EASYTOOL: Enhancing LLM-based Agents with Concise Tool Instruction](https://arxiv.org/pdf/2401.06201) 
		- 36 citations
	- [LLM With Tools: A Survey](https://arxiv.org/pdf/2409.18807)
		- 9 citations
	- [ReTool: Reinforcement Learning for Strategic Tool Use in LLMs](https://www.arxiv.org/abs/2504.11536)
		- This paper introduces **ReTool**, a framework that reimagines how models _learn_ to integrate computational tools like code interpreters into their reasoning. ReTool tackles this problem by treating tool use as a _skill to be learned_, not just mimicked, using outcome-driven RL ([Source: by cloud](https://mail.bycloud.ai/p/reasoning-models-can-be-effective-without-thinking?last_resource_guid=Post%3Ae5f10c5e-e495-4ba7-b94e-87b04ca267cb)).
		- 0 citations (SOTA)
- Blogs
	- [Routing in RAG-Driven Applications](https://medium.com/towards-data-science/routing-in-rag-driven-applications-a685460a7220)
	- [Building Custom Tools for LLM Agents](https://www.pinecone.io/learn/series/langchain/langchain-tools/)
## ART Framework
> Combining CoT prompting and tools in an interleaved manner has shown to be a strong and robust approach to address many tasks with LLMs. These approaches typically require hand-crafting task-specific demonstrations and carefully scripted interleaving of model generations with tool use. [Paranjape et al., (2023)(opens in a new tab)](https://arxiv.org/abs/2303.09014) propose a new framework that uses a frozen LLM to automatically generate intermediate reasoning steps as a program.
> 
> ART works as follows:
> 
> - given a new task, it select demonstrations of multi-step reasoning and tool use from a task library
> - at test time, it pauses generation whenever external tools are called, and integrate their output before resuming generation
> 
> ART encourages the model to generalize from demonstrations to decompose a new task and use tools in appropriate places, in a zero-shot fashion. In addition, ART is extensible as it also enables humans to fix mistakes in the reasoning steps or add new tools by simply updating the task and tool libraries.

