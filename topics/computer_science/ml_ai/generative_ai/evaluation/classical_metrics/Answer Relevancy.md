---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2024-10-24T11:41
modified: 2025-11-08T18:12
published:
sources:
  - "[Pinecone](https://github.com/pinecone-io/examples/blob/master/learn/generation/better-rag/03-ragas-evaluation.ipynb), [Ragas Answer Relevance](https://docs.ragas.io/en/v0.1.21/concepts/metrics/answer_relevance.html)"
topics:
  - Answer Relevancy
  - RAGAS
  - RAG Evaluation
authors:
ai-assisted:
hidden:
public: true
---
# Answer Relevancy
> Answer relevancy is our final metric. It focuses on the generation component and is similar to our "context precision" metric in that it measures how much of the returned information is relevant to our original question.
> 
> We return a low answer relevancy score when:
> - Answers are incomplete.
> - Answers contain redundant information.
> 
> A high answer relevancy score indicates that an answer is concise and does not contain "fluff" (ie irrelevant information).
> 
> The score is calculated by asking an LLM to generate multiple questions for a generated answer and then calculating the cosine similarity between the original question and the generated questions. Naturally, if we have a concise answer that answers a very specific question, we should find that the generated question will have a high cosine similarity to the original question.