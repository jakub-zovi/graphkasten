---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2025-03-19T17:12
modified: 2026-02-15T11:23
published:
sources:
  - "[Mixture of Experts Explained](https://huggingface.co/blog/moe#what-is-a-mixture-of-experts-moe), [Mixture of Experts vs. Transformers](https://www.linkedin.com/posts/avi-chawla_mixture-of-experts-vs-transformers-explained-activity-7300073933129584641-4f6q/)"
topics:
  - Transformers
authors:
ai-assisted:
hidden:
public: true
---
# Mixture of Experts (MoE)
 [Mixture of Experts Explained:
The scale of a model is one of the most important axes for better model quality. Given a fixed computing budget, training a larger model for fewer steps is better than training a smaller model for more steps.

Mixture of Experts enable models to be pretrained with far less compute, which means you can dramatically scale up the model or dataset size with the same compute budget as a dense model. In particular, a MoE model should achieve the same quality as its dense counterpart much faster during pretraining.

So, what exactly is a MoE? In the context of transformer models, a MoE consists of two main elements:
- **Sparse MoE layers** are used instead of dense feed-forward network (FFN) layers. MoE layers have a certain number of “experts” (e.g. 8), where each expert is a neural network. In practice, the experts are FFNs, but they can also be more complex networks or even a MoE itself, leading to hierarchical MoEs!
- A **gate network or router**, that determines which tokens are sent to which expert. For example, in the image below, the token “More” is sent to the second expert, and the token "Parameters” is sent to the first network. As we’ll explore later, we can send a token to more than one expert. How to route a token to an expert is one of the big decisions when working with MoEs - the router is composed of learned parameters and is pretrained at the same time as the rest of the network.
### MoEs TLDR
 [Mixture of Experts Explained:
- Are **pretrained much faster** vs. dense models
- Have **faster inference** compared to a model with the same number of parameters
- Require **high VRAM** as all experts are loaded in memory
- Face many **challenges in fine-tuning**, but [recent work](https://arxiv.org/pdf/2305.14705.pdf) with MoE **instruction-tuning is promising**


Figure source: [Mixture of Experts vs. Transformers](https://www.linkedin.com/posts/avi-chawla_mixture-of-experts-vs-transformers-explained-activity-7300073933129584641-4f6q/)
<img src="https://media.licdn.com/dms/image/v2/D5622AQEYHHJrLzzI6w/feedshare-shrink_1280/B56ZU8SiucGoAk-/0/1740473252446?e=1745452800&v=beta&t=rARxgtU9oVLmws_SHftgxtiIsIlYqO9Jb2MbaPDLVA0">