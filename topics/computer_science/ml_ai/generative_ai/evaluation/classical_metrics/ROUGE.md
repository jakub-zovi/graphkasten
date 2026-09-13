---
tags:
  - gen_ai
  - gen_ai/evaluation
created:
modified: 2026-02-28T17:23
published:
sources:
topics:
  - ROUGE
  - N-gram Metrics
  - Summarization Evaluation
authors:
ai-assisted:
hidden:
public: true
---
# Recall-Oriented Understudy for Gisting Evaluation (for N-grams)

## Definition


$$
 \text{ROUGE-N} = \frac{\sum_{S \in \{\text{Reference summaries}\}} \sum_{\text{gram}_n \in S} \text{Count}_{\text{match}}(\text{gram}_n)}{\sum_{S \in \{\text{Reference summaries}\}} \sum_{\text{gram}_n \in S} \text{Count}(\text{gram}_n)} 
$$
Or we can write it as an N-gram recall:
$$
\frac{\text{Total matching N-grams}}{\text{Total N-grams}}
$$
### Types of ROUGE: 
- **ROUGE-1**: Words (tokens) 
- **ROUGE-2**: Bigrams 
- **ROUGE-L**: Longest common subsequence 
- **ROUGE-Lsum**: Summary-level ROUGE-L