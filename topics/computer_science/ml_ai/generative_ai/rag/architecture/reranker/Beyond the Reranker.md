---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-07-03T10:00
modified: 2026-07-26T13:49
published: 2026-07-03
sources:
  - "[Beyond the Reranker (arXiv 2606.28367)](https://arxiv.org/abs/2606.28367)"
  - "[qarkapp/sscc-rag-paper](https://github.com/qarkapp/sscc-rag-paper)"
topics:
  - Reranking
  - RAG Enhancements
  - Retrieval Evaluation
authors:
  - Opus 4.8
ai-assisted: true
hidden: false
public: true
human-review: true
---
#### **Beyond the Reranker: Do RAG Retrieval Enhancements Help Once a Strong Reranker Is Present?**
- [Beyond the Reranker (arXiv 2606.28367)](https://arxiv.org/abs/2606.28367)
> This paper from Cascade Research asks if the many popular retrieval enhancements actually still help once you’ve added a strong cross-encoder reranker to a RAG pipeline? Most evidence for methods like query expansion, hierarchical summarization, graph expansion, routing, and rank fusion comes from homogeneous corpora (mostly Wikipedia prose), so the authors built HetDocQA, a benchmark whose collections mix code, markdown, prose, tables, and scientific PDFs. It uses character-span relevance labels matched to each system’s own chunks at evaluation time, which makes retrieval scores independent of how a system segments the corpus, and it splits data disjointly by collection so tuned thresholds can’t exploit recurring structure. They ran eight methods on a shared backbone (fixed embedder, reranker, and generator), paired HetDocQA with MuSiQue and QASPER as controls, and applied bootstrap confidence intervals with multiple-comparison correction. They find that the reranker carries almost all the retrieval quality, and beyond it only two methods give reliable gains: query expansion (HyDE), which helps when the question and evidence share little surface vocabulary, and SSCC, a per-source calibrated corrector that sets a separate acceptance threshold for each score source and helps only on heterogeneous data. Everything else that reranks or expands the candidate pool (RAPTOR, cross-document summarization, graph expansion, routing, rank fusion, corrective re-retrieval) shows no reliable improvement once the reranker is present, with the intuition being that a good reranker has already ordered a pool that contains the answer, leaving room to help only at the input (what enters the pool) and the answer decision (what gets accepted).

![](https://ci3.googleusercontent.com/meips/ADKq_Na3UabrGR9jGi4Jxi-M9PHXl8P8dxHLo72q-oNaHsBJhyCBeYxCjyiLoouCv2HRK0KcwJA1Dib61qXeYoxLNiHL2sZ8IYtVEh9cmekep0KMSKChRc13V9qA9GgTLcCr4YSSfG5NOXSMGzd0EUx78Qg1R48RzAJnTxNjAki090e1tK0ZiFBda4UZ66EuzGMHI7NDyHJygUS_AcD9YsMyzH3pQpZUm0AS7ZzaIA_PvYdeehgRIweg-6GjymIUiLJ3dmje_Y3znHFPuyg97l20Ump9eGJgw5Q9nLi9JAPJNQ4r8fKaYt6_oOQQzkL9Hfxz1p60Jrk=s0-d-e1-ft#https://substackcdn.com/image/fetch/$s_!ui4s!,w_1100,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F87ddfdd6-239d-444d-abdb-73f427be51f3_1613x619.png)