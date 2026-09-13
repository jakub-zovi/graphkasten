---
tags:
  - ml_ai
  - ml_ai/neural_nets
  - ml_ai/neural_nets/optimizers
created: 2026-01-14T11:09
modified: 2026-07-26T13:31
published:
sources:
topics:
  - Optimizers
  - Adaptive Learning Rate
  - Weight Decay
authors:
  - Jakub
ai-assisted: false
hidden:
public: true
---
# Optimizers
This note aggregates information about different optimizers used in neural networks.
## List
- [[AdaGrad]]
	- Adapts learning rate per-parameter via cumulative sum of squared gradients; effective for sparse features but suffers from monotonically decreasing LR.
- [[RMSProp]]
	- Fixes AdaGrad's vanishing LR via exponential moving average of squared gradients; precursor to Adam.
- [Adam](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FAdam) (Adaptive Moment Estimation)
	- A widely used, computationally efficient optimization algorithm for training deep learning models, combining the benefits of [[AdaGrad]] and [[RMSProp]].
- [Adamw](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FAdamw)
	- AdamW is a variant of Adam that decouples weight decay from the gradient-based update
- [Muon](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Foptimizers%2FMuon)
	- [Muon is scalable for LLM training](https://arxiv.org/pdf/2502.16982)
		- 2025-02-24
		- 47 citations
	- [Muon Outperforms Adam in Tail-End Associative Memory Learning](https://arxiv.org/pdf/2509.26030)
		- 2025-09-30
		- 2 citations
	- [From AdamW to Muon Optimizer](https://athekunal.medium.com/from-adamw-to-muon-optimizer-cf67d43fb9e9)
		- 2025-07-22

