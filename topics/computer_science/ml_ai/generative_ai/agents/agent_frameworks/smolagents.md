---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-03-13T10:13
modified: 2025-11-08T18:12
published:
sources:
  - "[smolagents](https://github.com/huggingface/smolagents), [smolagents-documentation](https://huggingface.co/docs/smolagents/index)"
topics:
authors:
ai-assisted:
hidden:
public: true
---
# smolagents
A minimalistic framework by Hugging Face that implements agents using [[Code Actions]] as opposed to traditional JSON/text approach. Code actions require secure sandbox environment for the code execution. This environment is implemented by the framework ([Secure code execution](https://huggingface.co/docs/smolagents/tutorials/secure_code_execution#secure-code-execution)).

[smolagents-documentation](https://huggingface.co/docs/smolagents/index):
> smolagents is a library that enables you to run powerful agents in a few lines of code. It offers:
> - ✨ Simplicity: the logic for agents fits in ~thousand lines of code. We kept abstractions to their minimal shape above raw code!
> - 🌐 Support for any LLM
> - 🧑‍💻 First-class support for Code Agents, i.e. agents that write their actions in code (as opposed to “agents being used to write code”).
> - 🤗 Hub integrations: you can share and load Gradio Spaces as tools to/from the Hub, and more is to come!

