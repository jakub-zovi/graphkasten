---
tags:
  - ml_ai
  - ml_ai/neural_nets
created:
modified: 2026-02-15T11:22
published:
sources:
  - "[Improving Language Understanding by Generative Pre-Training (2018)](https://hayate-lab.com/wp-content/uploads/2023/05/43372bfa750340059ad87ac8e538c53b.pdf)"
topics:
  - Transformers
  - GPT
authors:
ai-assisted:
hidden:
public: true
---
# Generative Pre-Trained Transformer
GPT was first introduced in the [Improving Language Understanding by Generative Pre-Training (2018)](https://hayate-lab.com/wp-content/uploads/2023/05/43372bfa750340059ad87ac8e538c53b.pdf) paper. GPT’s framework consists of two stages: [[GPT Pre-Training]] and [[GPT Fine-Tuning]].
One year later a [[GPT-2]] was introduced in the [Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf).

<img src="https://img1.daumcdn.net/thumb/R750x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGtXik%2Fbtq2qwxMQsS%2Fxj14YrCXfIpkmL6oU67by0%2Fimg.png">
## Key Contributions of GPT
- **Unsupervised Pre-training**: The model was trained on a large corpus of text using a **language modeling objective**. Essentially, the task was to predict the next word in a sequence, which allowed the model to learn useful language representations without requiring labeled data.
- **Supervised Fine-tuning**: After the pre-training phase, the model was fine-tuned on specific downstream tasks (like question-answering, sentiment analysis) with labeled data, and this process showed significant improvements in task-specific performance.