# Model Packaging Strategy (Unified Model Artifact)

This document explains how and why the project packages preprocessing,
feature engineering, and the trained model into a **single unified model
artifact**.



## 🎯 Problem Statement

During early iterations of this project, inference was implemented by
loading and applying multiple independent artifacts, including:

- The trained model
- A fitted imputer
- A fitted encoder
- Feature engineering logic executed in application code

While this approach worked functionally, it introduced several issues
as the system evolved toward a production-style setup.

Specifically, we observed the following risks:

- **Training–serving skew**, where preprocessing logic in the API could
  diverge from the logic used during training
- **Version mismatches** between preprocessing artifacts and the trained
  model when retraining or rolling back models
- **Tight coupling** between inference code and preprocessing
  implementation details, making the API harder to maintain and test




## ✅ Design Decision

This project packages **all inference-time logic** into a **single model
artifact**, which is then registered and versioned in MLflow.

A single model version represents:
- The exact preprocessing steps
- The exact feature engineering logic
- The exact trained model

Inference consumes **one object** and calls:

```python
model.predict(raw_input_df)
```

The model is unified using this approach:
- **MLflow PyFunc models**, which support custom model classes
- A custom `HousingInferencePipeline` class that encapsulates preprocessing and
  prediction logic.   
    - See [src/inference/pipeline.py](../../src/inference/pipeline.py) for details

---