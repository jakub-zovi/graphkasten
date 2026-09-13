---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-03-22T19:00
modified: 2026-08-01T11:05
published:
sources:
  - "[Sentence Transformers Training Overview](https://sbert.net/docs/sentence_transformer/training_overview.html)"
  - "[Bi-Encoder Training — Sentence Transformers](https://sbert.net/examples/sentence_transformer/training/README.html)"
  - "[Training and Fine-Tuning — HuggingFace SBERT](https://huggingface.co/sentence-transformers)"
topics:
  - Bi-Encoder
  - Fine-tuning
  - Loss Functions
authors:
  - Jakub
ai-assisted: true
hidden:
public: true
human-review: true
---
# Bi-Encoder Fine-tuning

![|400](BiEncoder.png)

- Fine-tuning a bi-encoder adapts the embedding space so that semantically related (query, document) pairs end up close together
- Practical companion to [[Bi-encoder training]] which covers the theoretical backpropagation mechanics

## Architecture
- Two transformer encoders with **shared weights** (typically BERT / RoBERTa / MiniLM)
- Pooling: mean pooling over token embeddings (default) or `[CLS]` token
- Similarity: dot product or cosine similarity between query and document vectors
- No joint encoding — query and document vectors are computed independently; enables precomputing a document index

## Training Data Formats
- **Positive pairs** `(query, doc+)` — used with in-batch negatives; most common and efficient format
- **Triplets** `(query, doc+, doc-)` — explicit hard negatives; stronger signal per sample
- **Scored pairs** `(query, doc, score)` — continuous label (0–1); used for regression-style or distillation losses

## Primary Loss — [[MultipleNegativesRankingLoss]] (MNR / InfoNCE)
- All other documents in the batch are treated as negatives for each query — no explicit negative mining needed
- Scales well with batch size: larger batch = more negatives = stronger gradient signal
- **Dominant choice for retrieval fine-tuning** in sentence-transformers; works out of the box with (anchor, positive) pairs

$$
\mathcal{L} = -\frac{1}{B} \sum_{i=1}^{B} \log \frac{\exp(s(\mathbf{q}_i, \mathbf{d}_i) / \tau)}{\sum_{j=1}^{B} \exp(s(\mathbf{q}_i, \mathbf{d}_j) / \tau)}
$$

where $B$ is the batch size, $\tau$ is the temperature, and $s(\mathbf{q}, \mathbf{d})$ is cosine or dot-product similarity.

```python
from datasets import Dataset
from sentence_transformers import SentenceTransformer
from sentence_transformers.losses import MultipleNegativesRankingLoss
from sentence_transformers.training_args import SentenceTransformerTrainingArguments
from sentence_transformers.trainer import SentenceTransformerTrainer

model = SentenceTransformer("sentence-transformers/all-MiniLM-L6-v2")

train_dataset = Dataset.from_dict({
    "anchor": ["What is Python?", "Capital of France?"],
    "positive": ["Python is a high-level programming language.", "Paris is the capital of France."],
})

	loss = MultipleNegativesRankingLoss(model)

args = SentenceTransformerTrainingArguments(
    output_dir="output/mnr-finetuned",
    num_train_epochs=3,
    per_device_train_batch_size=64,   # larger = more in-batch negatives
    warmup_ratio=0.1,
    fp16=True,
)

trainer = SentenceTransformerTrainer(
    model=model,
    args=args,
    train_dataset=train_dataset,
    loss=loss,
)
trainer.train()
```

## Alternative Losses
- **`CachedMultipleNegativesRankingLoss`** — memory-efficient version using gradient caching; allows very large effective batch sizes without OOM; recommended when GPU memory is limited
- [[TripletLoss]] — $\mathcal{L} = \max(0, \text{sim}(q, d^-) - \text{sim}(q, d^+) + margin)$; requires explicit hard negatives per sample; less data-efficient than MNR but gives explicit control over negatives
- **`MarginMSELoss`** — aligns bi-encoder scores to teacher (cross-encoder) scores; effective for two-stage distillation pipelines where a slower but stronger cross-encoder provides soft labels
- **`CosineSimilarityLoss`** — MSE between predicted cosine and a continuous label (0–1); suited for STS/semantic similarity tasks, generally weaker for retrieval
- **`ContrastiveLoss`** — pulls positive pairs together and pushes negative pairs apart by a margin; older approach, superseded by MNR for most retrieval tasks

## Hard Negative Mining
- Random negatives (in-batch) are easy but weak — model quickly learns to distinguish them
- Hard negatives significantly improve training efficiency:
  - **BM25** — retrieve top-k lexically similar docs, pick non-relevant ones as negatives
  - **Cross-encoder rescoring** — score BM25 candidates with a cross-encoder, use low-scoring ones as hard negatives
  - **ANN index** — use the current bi-encoder to find nearest neighbours; non-relevant ones are hard negatives (requires periodic index refresh)

## Datasets
- **MS MARCO passage ranking** — large-scale query–passage pairs with relevance labels; primary benchmark
- **Natural Questions (NQ)** — Wikipedia-based open-domain QA pairs
- **TriviaQA** — trivia questions with supporting evidence passages
- **BEIR benchmark** — heterogeneous retrieval benchmark across 18 domains; used for zero-shot evaluation

## Tips
- Use `CachedMultipleNegativesRankingLoss` if batch size is limited by GPU memory
- Combine hard negatives with in-batch negatives for best results
- For domain adaptation, fine-tune on (query, relevant passage) pairs mined from the target corpus via BM25 + human/model annotation
- Two-stage training: first MNR on large generic corpus, then `MarginMSELoss` distillation from a cross-encoder on domain-specific data