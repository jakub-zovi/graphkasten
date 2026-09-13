---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-03-02T16:24
modified: 2026-03-22T19:04
published:
sources:
  - "[2026-02-27 - Information Retrieval Papers](https://recsys.substack.com/p/benchmarking-retrieval-and-re-ranking?utm_source=post-email-title&publication_id=1662831&post_id=189335924&utm_campaign=email-post-title&isFreemail=true&r=53sn48&triedRedirect=true&utm_medium=email)"
  - "[How Retrieved Context Shapes Internal Representations in RAG](https://arxiv.org/abs/2602.20091](https://arxiv.org/abs/2602.20091)"
topics:
  - RAG Interpretability
  - LLM Internal Representations
  - Retrieval Analysis
  - Abstention
authors:
ai-assisted:
hidden:
public: true
---
# How Retrieved Context Shapes Internal Representations in RAG
This paper from WISC investigates how retrieved documents in RAG systems shape the internal hidden representations of LLMs. Using four QA datasets and three LLMs, the authors classify retrieved documents into relevant, distracting, and random categories, then analyze last-prompt-token representations via PCA under controlled single- and multi-document settings. They share the following major findings:

1. Random documents cause the largest representation drift (even larger than relevant or distracting ones), and this drift is tightly correlated with abstention behavior.
    
2. Relevant documents barely shift representations at all, acting mainly as confidence boosters for queries the model can already answer rather than injecting genuinely new information, which explains why RAG struggles on hard queries.
    
3. In multi-document settings, even a single relevant document anchors the representation and suppresses noise from accompanying distractors or random docs.
    
4. Layer-wise analysis shows that models detect coarse semantic mismatches (random context) early on but can’t reliably separate relevant from distracting documents until much later layers.
    
5. Later layers progressively favor parametric knowledge over retrieved evidence, which stabilizes generation for easy queries but fundamentally limits RAG’s ability to override insufficient internal knowledge on harder ones.
    

The practical conclusion is that aggressive document filtering may be unnecessary when at least one relevant document is present, and current RAG architectures have a built-in ceiling on how much retrieved evidence can actually influence model behavior.


![](https://substackcdn.com/image/fetch/$s_!E_9g!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F623c65df-aa78-4945-856c-2cc57f1613d2_1525x758.png)
