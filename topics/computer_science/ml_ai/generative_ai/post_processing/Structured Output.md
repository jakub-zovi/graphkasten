---
tags:
  - gen_ai
  - gen_ai/agents
created: 2024-10-14T22:35:00
modified: 2026-04-07T09:28
published:
sources:
topics:
  - "[Structured outputs in LLMs](https://www.leewayhertz.com/structured-outputs-in-llms/)"
  - "[Prompting vs JSON Mode vs Function Calling vs Constrained Generation vs SAP](https://boundaryml.com/blog/schema-aligned-parsing#sap)"
authors:
ai-assisted:
hidden:
public: true
---
# Structured Output
## Types of Structured Output
(Source: [Prompting vs JSON Mode vs Function Calling vs Constrained Generation vs SAP](https://boundaryml.com/blog/schema-aligned-parsing#sap))
> The most common way to extract structured data / do function calling out of an LLM is to somehow get the LLM to output JSON, and then call JSON.parse.
> 
> However, there is no reason to assume that JSON, the prevalant serialization for Web APIs, should be the ideal serialization for LLMs. Given the stochastic nature of LLMs, it might even be true that all strict serialization formats are suboptimal, since a single error can cause the entire serialization to be invalid.
- Different ways of extracting structured output
	- [[Prompting]]
	- [[JSON Mode]]
	- [[Constrained Generation]]
	- [[Schema Aligned Parsing]] (SAP)
## Structured Output Generation
[Structured outputs in LLMs](https://www.leewayhertz.com/structured-outputs-in-llms/):
> When we need the LLM to generate text in a specific format, like JSON, we can’t just let it pick any token. We need to ensure that every token it selects follows the rules of that format. This is where the concept of a Finite State Machine (FSM) comes into play.
### What is a Finite State Machine (FSM)?
[Structured outputs in LLMs](https://www.leewayhertz.com/structured-outputs-in-llms/):
> The Finite State Machine (FSM) plays a crucial role in guiding the generation process of a Large Language Model (LLM) when producing structured outputs. Here’s how it works:
> 
> As the LLM generates text, it does so one token at a time, progressing through various states in the FSM. Each state represents a specific point in the generation process, corresponding to a part of the desired structure (e.g., JSON or XML format). The FSM determines which transitions, or token choices, are valid for each state based on the predefined structure. By calculating these permissible transitions, the FSM can identify which tokens are acceptable as the “next step” in the sequence.
> 
> During the decoding phase, the FSM tracks the current state of the LLM’s output. It then filters out any tokens that don’t fit the required format by applying a technique known as logit bias. This involves adjusting each token’s probabilities (logits), significantly reducing the likelihood of invalid tokens being selected. As a result, the LLM is guided to generate only tokens consistent with the specified structure, ensuring the output adheres to the desired format. This approach enhances the generated content’s accuracy and ensures it aligns perfectly with the expected structured output.
## Providers Support
### OLlama
Source: [Structured outputs](https://ollama.com/blog/structured-outputs)
> Ollama now supports structured outputs making it possible to constrain a model’s output to a specific format defined by a JSON schema. The Ollama Python and JavaScript libraries have been updated to support structured outputs.
### OpenAI
OpenAI announced [Structured Outputs for its API](https://openai.com/index/introducing-structured-outputs-in-the-api/), a feature that allows users to specify the fields and schema of extracted data, and guarantees that the JSON output will follow that specification.

Demo of using this capability: [README.openai-structured-output-demo.md](https://gist.github.com/dannguyen/faaa56cebf30ad51108a9fe4f8db36d8)
## Libraries
- [[Outlines Library]]
	- A library specifically focused on structured text generation from LLMs