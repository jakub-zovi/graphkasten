---
tags:
  - gen_ai
  - gen_ai/agents
created: 2025-02-03T13:05
modified: 2025-08-09T14:35
published:
sources:
topics:
authors:
ai-assisted:
hidden:
public: true
---
# Query Routing
Query routing can be defined as action where "LLM output determines basic control flow". A task of identifying whether a system should use stronger or weaker LLM model to answer the query, is also call sometimes as query routing, but more appropriate name for it is [[Model Routing]]. 
## Custom Query Routing Approaches
- Text classification with fine-tuned BERT
- [SetFit](https://huggingface.co/docs/setfit/index) few-shot classification through embedding fine-tuning
	- [[SetFit]] is an efficient and prompt-free framework for few-shot fine-tuning of [Sentence Transformers](https://sbert.net/). It achieves high accuracy with little labeled data - for instance, with only 8 labeled examples per class on the Customer Reviews sentiment dataset, 🤗 SetFit is competitive with fine-tuning RoBERTa Large on the full training set of 3k examples!
- [Aurelio](https://www.aurelio.ai/semantic-router) - open-source library for semantic routing  (probably uses SetFit, need to investigate)
- [Classify - Cohere](https://docs.cohere.com/v2/reference/classify) - classification through Cohere service that probably uses SetFit in the background
- [Route0x](https://github.com/PrithivirajDamodaran/Route0x) - very few stars on Github but might be worth looking into
	- [X post](https://x.com/prithivida/status/1857758598891450868)