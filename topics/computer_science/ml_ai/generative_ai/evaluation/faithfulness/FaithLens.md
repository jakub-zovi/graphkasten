---
tags:
  - gen_ai
  - gen_ai/evaluation
created: 2026-06-08T10:00
modified: 2026-07-26T13:41
published: 2025-12-25
sources:
  - "[S1s-Z/FaithLens](https://github.com/S1s-Z/FaithLens)"
  - "[FaithLens paper (arXiv:2512.20182)](https://arxiv.org/abs/2512.20182)"
topics:
  - Grounded Fact Verification
  - Evaluation
authors:
  - Opus 4.7
ai-assisted: true
hidden:
public: true
human-review: true
---
# FaithLens
- Resources
	- Paper: [FaithLens (Si et al., 2025)](https://arxiv.org/abs/2512.20182)
		- ACL 2026
	- GitHub: [S1s-Z/FaithLens](https://github.com/S1s-Z/FaithLens)
	- Model: [ssz1111/FaithLens](https://huggingface.co/ssz1111/FaithLens)
- 8B specialized faithfulness classifier that, unlike Bespoke-MiniCheck-7B, also returns a **natural-language justification** alongside the label.
## What It Does
- Dual task per `(document, claim)`:
	1. **Predict** whether the claim is faithful or hallucinated wrt the document
	2. **Explain** the prediction in human-readable text
- Authors report the 8B model outperforming larger general-purpose LLMs (GPT-5.2, o3) on 12 grounding benchmarks including [[LLM-AggreFact]] and HoVer.
![FaithLens overview|600](https://github.com/S1s-Z/FaithLens/raw/master/images/intro.png)
## Training Recipe
- **Two-stage** pipeline:
	1. **Cold-start SFT** on synthetic `(doc, claim, label, explanation)` data
	2. **Rule-based RL** rewarding both prediction accuracy and explanation quality
- The explanation channel is what differentiates FaithLens from MiniCheck-style binary classifiers - useful when downstream users need to know **why** a claim was flagged, not just that it was.
![FaithLens training|600](https://github.com/S1s-Z/FaithLens/raw/master/images/training.png)
## Why It Matters
- For audit / compliance flows where a "0/1 hallucinated" verdict is not enough.
- For Claim Decomposition pipelines that want to surface the exact missing/contradicting evidence to the end user rather than just suppressing the answer.
