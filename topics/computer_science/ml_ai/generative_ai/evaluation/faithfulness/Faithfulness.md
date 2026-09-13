---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2024-10-24T11:36
modified: 2026-06-25T09:53
published:
sources:
  - "[Pinecone](https://github.com/pinecone-io/examples/blob/master/learn/generation/better-rag/03-ragas-evaluation.ipynb), [Ragas Faithfulness](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/faithfulness/)"
topics:
  - Faithfulness
  - RAGAS
  - LLM-as-Judge
  - RAG Evaluation
authors:
ai-assisted:
hidden:
public: true
---
# Faithfullness
- Beyond the RAGAS LLM-as-a-judge formulation below, faithfulness can also be scored with cheap specialized classifiers
> The _faithfullness_ metric measures (from _0_ to _1_) the factual consistency of an answer when compared to the retrieved context. A score of _1_ means all claims in the answer can be found in the context. A score of _0_ would indicate _no_ claims in the answer are found in the context.
> 
> We calculate the faithfullness like so:
> $$
Faithfulness = \frac{\text{Number of claims in answer also found in context}}{\text{Number of claims in answer}}
 $$
> 
> When calculating faithfullness RAGAS is using OpenAI LLMs to decide which claims are in the answer and whether they also exist in the context. Because of the "generative" nature of this approach we won't always get accurate scores.
> 
> We can see that we get perfect scores for all but our fourth result, which scores `0.0`. However, when looking at this we can see some claims that seem related. Nonetheless the fourth answer does seem to be less grounded in the truth of our context than other responses, indicated that there is justification behind this low score.