---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-10-21T19:16
modified: 2026-02-15T11:22
published:
sources:
  - "[Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)"
topics:
  - Transformers
  - GPT
authors:
ai-assisted:
hidden:
public: true
---
# GPT-2
- GPT-2 was first introduced in the [Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf).
- ChatGPT[^1]:
> The **"Language Models are Unsupervised Multitask Learners"** paper, published in 2019, introduced the successor to GPT: **GPT-2**. GPT-2 marked a major leap in both scale and capabilities. The key innovations and insights in this paper were:
> 
> - **Scale**: GPT-2 was a much larger model compared to GPT. It had 1.5 billion parameters, compared to the 117 million parameters in the original GPT. This increase in model size allowed it to learn richer patterns from data.
> - **Unsupervised Multitask Learning**: Unlike GPT, GPT-2 was not fine-tuned on individual tasks. Instead, it demonstrated **zero-shot, few-shot, and multitask learning** abilities. This meant GPT-2 could perform tasks like question answering, translation, and summarization without any task-specific fine-tuning, simply by being prompted in natural language. It used its internal representations learned during pre-training to generalize to these new tasks.
>     - **Zero-shot learning**: The ability of GPT-2 to handle tasks it had not been explicitly trained on.
>     - **Few-shot learning**: The ability to generalize well with minimal examples or instructions for a new task.
>     - **Multitask learning**: GPT-2 could perform many different tasks based solely on the type of input it was given, without needing separate task-specific architectures.
> 
> The most significant shift introduced in the GPT-2 paper was the realization that a sufficiently large language model could be **task-agnostic**, meaning it could generalize to a wide range of NLP tasks without being explicitly trained for them.

[^1]: Prompt: What Language Models are Unsupervised Multitask Learners papers introduced? How does it relate to the original GPT paper called Improving Language Understanding by Generative Pre-Training?