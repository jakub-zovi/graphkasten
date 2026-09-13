---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2026-03-26T00:00
modified: 2026-07-26T13:36
published:
sources:
  - "[Attention Residuals (ArXiv 2603.15031)](https://arxiv.org/abs/2603.15031)"
  - "[MoonshotAI/Attention-Residuals (GitHub)](https://github.com/MoonshotAI/Attention-Residuals)"
topics:
  - Residual Connections
  - Attention Mechanism
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Attention Residuals (AttnRes)
- Drop-in replacement for standard [Residual Blocks](obsidian://open?vault=graphkasten&file=topics%2Fcomputer_science%2Fml_ai%2Fneural_networks%2Fcomponents%2FResidual%20Blocks) in Transformers, developed by the Kimi Team (MoonshotAI)
- Replaces fixed, uniform skip-connection accumulation with **learned, input-dependent softmax attention over earlier layer outputs**

## Problem With Standard Residuals
- **Dilution of layer contributions** — all prior layers are weighted equally regardless of relevance
- **Unbounded magnitude growth** — hidden-state norms grow without constraint as depth increases, causing training instability in deep networks

## Mechanism
### Full AttnRes
- Each layer $l$ computes a weighted sum over all previous hidden states $\{h_0, h_1, \dots, h_{l-1}\}$
- Attention weights $\alpha_l$ are input-dependent and learned via softmax:
$$
h_l = \sum_{i=0}^{l-1} \alpha_{l,i} \cdot h_i + \mathcal{F}_l(h_{l-1})
$$
where $\alpha_{l,i} = \text{softmax}(\mathbf{q}_l \cdot \mathbf{k}_i^T)$
- Memory complexity: $O(Ld)$ — stores all layer outputs

### Block AttnRes (Practical Variant)
- Groups $L$ layers into $N$ blocks (e.g. $N \approx 8$)
- Standard residuals are used **within** each block
- Attention residuals are applied **between** block-level summary representations
- Memory: $O(Nd)$ — only block summaries are retained
- Recovers most of Full AttnRes gains while being production-deployable

## Key Results
- **Scaling laws:** Block AttnRes achieves the same loss as the baseline using **1.25× less compute** (equivalently, same compute yields a lower-loss model)
- **Downstream benchmarks** (Kimi Linear 48B, 3B activated, 1.4T tokens):
  - GPQA-Diamond: **+7.5** (largest gain, reasoning tasks)
  - HumanEval: **+3.1** (coding)
  - Consistent improvements on MMLU, GSM8K, and Chinese benchmarks
- **Training dynamics:** bounded output magnitudes across depth, more uniform gradient distribution across layers
