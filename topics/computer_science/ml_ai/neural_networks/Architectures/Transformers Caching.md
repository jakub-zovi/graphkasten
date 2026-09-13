---
tags:
  - ml_ai
  - ml_ai/neural_nets
created: 2024-11-11T10:38
modified: 2026-02-15T10:16
published:
sources:
  - "[Cache strategies](https://huggingface.co/docs/transformers/en/kv_cache)"
topics:
  - Transformers
authors:
ai-assisted:
hidden:
public: true
---
# Transformers Caching
The key-value (KV) vectors are used to calculate attention scores. For autoregressive models, KV scores are calculated _every_ time because the model predicts one token at a time. Each prediction depends on the previous tokens, which means the model performs the same computations each time.

A KV _cache_ stores these calculations so they can be reused without recomputing them. Efficient caching is crucial for optimizing model performance because it reduces computation time and improves response rates. Refer to the [Caching](https://huggingface.co/docs/transformers/en/cache_explanation) doc for a more detailed explanation about how a cache works.

Transformers offers several [Cache](https://huggingface.co/docs/transformers/v5.1.0/en/internal/generation_utils#transformers.Cache) classes that implement different caching mechanisms. Some of these [Cache](https://huggingface.co/docs/transformers/v5.1.0/en/internal/generation_utils#transformers.Cache) classes are optimized to save memory while others are designed to maximize generation speed. Refer to the table below to compare cache types and use it to help you select the best cache for your use case.

| Cache Type          | Supports sliding layers | Supports offloading | Supports torch.compile() | Expected memory usage |
| ------------------- | ----------------------- | ------------------- | ------------------------ | --------------------- |
| [[Dynamic Cache]]   | Yes                     | Yes                 | No                       | Medium                |
| [[Static Cache]]    | Yes                     | Yes                 | Yes                      | High                  |
| [[Quantized Cache]] | No                      | No                  | No                       | Low                   |

This guide introduces you to the different [Cache](https://huggingface.co/docs/transformers/v5.1.0/en/internal/generation_utils#transformers.Cache) classes and shows you how to use them for generation.