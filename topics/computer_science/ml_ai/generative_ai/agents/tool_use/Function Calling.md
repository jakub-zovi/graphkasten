---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-02-03T17:44
modified: 2026-07-21T09:05
published:
sources:
  - "[Function Calling with LLMs](https://www.promptingguide.ai/applications/function_calling), [OpenAI Function calling](https://platform.openai.com/docs/guides/function-calling?api-mode=chat)"
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Function Calling
- [Function Calling with LLMs](https://www.promptingguide.ai/applications/function_calling)
> Function calling is the ability to reliably connect LLMs to external tools to enable effective tool usage and interaction with external APIs.
> 
> LLMs like GPT-4 and GPT-3.5 have been fine-tuned to detect when a function needs to be called and then output JSON containing arguments to call the function. The functions that are being called by function calling will act as tools in your AI application and you can define more than one in a single request.
- Function calling can be considered just different name for [[Tool Calling]]. Only difference is that the tools can be defined by developer and are not integrated within chat bot interface such is the case for ChatGPT UI.
## OpenAI
Source: [OpenAI Function calling](https://platform.openai.com/docs/guides/function-calling?api-mode=chat)
## Under the hood
Under the hood, functions are injected into the system message in a syntax the model has been trained on. **This means functions count against the model's context limit and are billed as input tokens.** If you run into token limits, we suggest limiting the number of functions or the length of the descriptions you provide for function parameters.
It is also possible to use [fine-tuning](https://platform.openai.com/docs/guides/fine-tuning#fine-tuning-examples) to reduce the number of tokens used if you have many functions defined in your tools specification.
## With Reasoning
[Reasoning models](https://platform.openai.com/docs/guides/reasoning?api-mode=responses#keeping-reasoning-items-in-context):
> **Keeping reasoning items in context**
> When doing [function calling](https://platform.openai.com/docs/guides/function-calling) with a reasoning model in the [Responses API](https://platform.openai.com/docs/apit-reference/responses), we highly recommend you pass back any reasoning items returned with the last function call (in addition to the output of your function). If the model calls multiple functions consecutively, you should pass back all reasoning items, function call items, and function call output items, since the last `user` message. This allows the model to continue its reasoning process to produce better results in the most token-efficient manner.
## Best Practices
1. **Write clear and detailed function names, parameter descriptions, and instructions.**
    - **Explicitly describe the purpose of the function and each parameter** (and its format), and what the output represents.
    - **Use the system prompt to describe when (and when not) to use each function.** Generally, tell the model _exactly_ what to do.
    - **Include examples and edge cases**, especially to rectify any recurring failures. (**Note:** Adding examples may hurt performance for [reasoning models](https://platform.openai.com/docs/guides/reasoning).)
2. **Apply software engineering best practices.**
    - **Make the functions obvious and intuitive**. ([principle of least surprise](https://en.wikipedia.org/wiki/Principle_of_least_astonishment))
    - **Use enums** and object structure to make invalid states unrepresentable. (e.g. `toggle_light(on: bool, off: bool)` allows for invalid calls)
    - **Pass the intern test.** Can an intern/human correctly use the function given nothing but what you gave the model? (If not, what questions do they ask you? Add the answers to the prompt.)
3. **Offload the burden from the model and use code where possible.**
    - **Don't make the model fill arguments you already know.** For example, if you already have an `order_id` based on a previous menu, don't have an `order_id` param – instead, have no params `submit_refund()` and pass the `order_id` with code.
    - **Combine functions that are always called in sequence.** For example, if you always call `mark_location()` after `query_location()`, just move the marking logic into the query function call.
4. **Keep the number of functions small for higher accuracy.**
    - **Evaluate your performance** with different numbers of functions.
    - **Aim for fewer than 20 functions** at any one time, though this is just a soft suggestion.
5. **Leverage OpenAI resources.**
    - **Generate and iterate on function schemas** in the [Playground](https://platform.openai.com/playground).
    - **Consider [fine-tuning](https://platform.openai.com/docs/guides/fine-tuning) to increase function calling accuracy** for large numbers of functions or difficult tasks. ([cookbook](https://cookbook.openai.com/examples/fine_tuning_for_function_calling))