---
tags:
  - cs
  - cs/data_eng
created: 2024-10-07T14:47
modified: 2026-08-01T10:55
published:
sources:
  - "[Feature Store](https://www.databricks.com/product/feature-store)"
topics:
  - Databricks
  - Feature Store
  - MLflow
authors:
ai-assisted:
hidden:
public: true
---
# Feature Store
- [Feature Store](https://www.databricks.com/product/feature-store)
> Provide data teams with the ability to create new features, explore and reuse existing ones, publish features to low-latency online stores, build training data sets and retrieve feature values for batch inference.
- I do not see many benefits in it except for the option of tracking which notebook generated which feature. It should also be more easily integrated with MlFlow ([src](https://community.databricks.com/t5/machine-learning/what-are-the-practical-advantage-of-feature-store-compared-to/td-p/10281)). Additionally, it has nice UI. In background it is build on top of delta tables.