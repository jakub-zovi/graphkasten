---
tags:
  - cs
  - cs/databases
created: 2025-04-14T15:56
modified: 2026-08-01T10:50
published:
sources:
topics:
  - Linear Combination
  - Rank Fusion
  - Score Normalization
authors:
  - ChatGPT
ai-assisted: true
hidden:
public: true
human-review: true
---
## Problems With Linear Combination
(ChatGPT[^1])
### 1. Inconsistent Score Scales
Each ranking system might use a **different scoring mechanism**:
- One system might output scores between 0 and 1 (e.g., probability).
- Another might produce raw dot-product scores (e.g., from a transformer model).
- A third might score relevance between 0 and 100.
### 2. Difficult Normalization
To fix the above, you’d normalize the scores (e.g., z-score, min-max, softmax), but:
- **Score distributions are often skewed**, especially in IR.
- Some methods produce **score ties or flat distributions**, making normalization unstable.
- **Document sets vary per query**, so per-query normalization might not generalize well.
### 3. Sensitivity to Weights
Linear combination relies on **weights** for each ranking (e.g., 0.3 for system A, 0.7 for system B). But:
- It’s not always clear how to **choose these weights**.
- Small errors in weighting can cause **unexpected drops in performance**.
- If one ranking is noisy, even a small weight can **pull down** the overall quality.
### 4. Poor Performance with Partial or Weak Rankers
If one ranker doesn’t rank certain documents at all (e.g., it truncates after top-100), those documents might receive a **zero or missing score**, and be unfairly penalized—even if other systems rank them highly.

---

[^1]: Prompt: "Can you elaborate why pure linear combination should not be used for combination of the different rankings?"