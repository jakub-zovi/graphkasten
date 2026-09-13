---
tags:
  - gen_ai
  - gen_ai/rag
created: 2026-03-22T19:00
modified: 2026-08-01T11:06
published:
sources:
  - "[Cross-Encoder Training Overview — Sentence Transformers](https://sbert.net/docs/cross_encoder/training_overview.html)"
  - "[Training and Fine-Tuning Cross Encoders — Sentence Transformers](https://sbert.net/examples/cross_encoder/training/README.html)"
topics:
  - Cross-Encoder
  - Fine-tuning
  - Loss Functions
authors:
ai-assisted: true
hidden:
public: true
human-review: true
---
# Cross-Encoder Training

![|400](CrossEncoder.png)

- Fine-tuning a cross-encoder adapts the model to a specific domain by teaching it which (query, document) pairs are relevant
- The model sees both texts in a single forward pass, so gradients flow through the full pair directly — no special contrastive setup needed

## Architecture
- Backbone: BERT / RoBERTa / MiniLM transformer encoder
- Input: `[CLS] query [SEP] document [SEP]`
- Head: linear layer on `[CLS]` → scalar logit
- For binary classification: sigmoid applied to logit; for ranking: raw logit used as score

## Training Data Formats
- **Binary pairs** `(query, doc, label)` — label ∈ {0, 1}; most common format (positive/negative pairs)
- **Soft-label pairs** `(query, doc, score)` — continuous relevance score (e.g. 0.0–1.0); useful for distillation
- **Triplets** `(query, doc+, doc-)` — pairwise format; model must assign higher score to `doc+`

## Primary Loss — `BinaryCrossEntropyWithLogitsLoss`
- Standard loss for binary relevance labels
- Applies sigmoid to the raw logit then computes cross-entropy against the {0, 1} label
- Most widely used for domain adaptation of cross-encoders
- Works directly with sentence-transformers `CrossEncoder` class

$$
\mathcal{L} = -\frac{1}{N} \sum_{i=1}^{N} \left[ y_i \log \sigma(s_i) + (1 - y_i) \log (1 - \sigma(s_i)) \right]
$$

where $s_i$ is the raw logit and $y_i \in \{0, 1\}$ is the label.

```python
from sentence_transformers.cross_encoder import CrossEncoder
from sentence_transformers.cross_encoder.losses import BinaryCrossEntropyLoss
from sentence_transformers import InputExample
from torch.utils.data import DataLoader

model = CrossEncoder("cross-encoder/ms-marco-MiniLM-L-6-v2", num_labels=1)

train_samples = [
    InputExample(texts=["What is Python?", "Python is a programming language"], label=1.0),
    InputExample(texts=["What is Python?", "The Eiffel Tower is in Paris"], label=0.0),
]

train_dataloader = DataLoader(train_samples, shuffle=True, batch_size=16)
loss = BinaryCrossEntropyLoss(model)

model.fit(
    train_dataloader=train_dataloader,
    loss_fct=loss,
    epochs=3,
    warmup_steps=100,
)
```

## Alternative Losses
- **`MSELoss`** — for soft/continuous relevance scores; useful when labels are real-valued judgements
- **`MarginMSELoss`** — knowledge distillation from a teacher model; minimises $(s_{\text{teacher}} - s_{\text{cross}})^2$ with a margin; preferred when soft labels come from BM25 or a stronger cross-encoder
- **`RankingLoss` / `RankNetLoss`** — pairwise loss; ensures $\text{score}(q, d^+) > \text{score}(q, d^-)$ by a margin; needs triplet data
- **`ListNetLoss` / `ListMLELoss`** — listwise losses; operate over the full ranked list; stronger signal but need more data

## Datasets
- **MS MARCO passage ranking** — 500k+ (query, passage, label) pairs; standard benchmark and fine-tuning corpus
- **MS MARCO document ranking** — larger documents version
- **SNLI / NLI datasets** — for pretraining on entailment/contradiction as a proxy for relevance
- **Domain-specific pairs** — labelled by annotators or mined via BM25 + negative sampling

## Tips
- Start from a pretrained cross-encoder checkpoint (e.g. `cross-encoder/ms-marco-MiniLM-L-6-v2`) rather than raw BERT for retrieval tasks — less data needed
- Use hard negatives (BM25 top results that are not relevant) rather than random negatives for faster learning
- Combine with bi-encoder fine-tuning in a two-stage pipeline: bi-encoder retrieves, cross-encoder rescores
