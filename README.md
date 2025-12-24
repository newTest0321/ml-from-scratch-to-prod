# ML from Scratch to Production

An end-to-end **Machine Learning engineering project** that demonstrates how a
model evolves from **experimentation** to **production-ready pipelines and
serving systems**.

The project uses the **California Housing dataset** as a reference use case and
focuses on building a **clean, reproducible, and deployable ML system** with
clear separation between:

* experimentation
* training pipelines
* inference (batch & online)
* MLOps concerns


## 🎯 What This Repository Represents

This repository is structured to show the **progressive evolution** of an ML
project, not just the final state.

It demonstrates:

* ML experimentation and reasoning
* Migration from notebooks to pipelines
* Batch inference workflows
* A production-style **FastAPI online inference service**
* Clean separation between training, tracking, and serving


## 🌿 Branch Overview

This repository uses **multiple branches** to represent different stages of
maturity.

### 🔹 `ml-baseline` — ML Experimentation

Purpose:

* Model experimentation and feature exploration
* Notebook-driven workflows
* ML reasoning and evaluation

Includes:

* Jupyter notebooks
* ML-focused documentation
* Multiple model experiments

This branch answers:
**“How was the model chosen?”**

---

### 🔹 `api-baseline` — Serving Without MLflow

Purpose:

* Introduce batch inference and an API
* Use filesystem-based artifacts
* Focus on serving logic, not MLOps tooling

Includes:

* Training and inference pipelines
* FastAPI-based online inference
* Local artifact loading
* Dockerized API

This branch answers:
**“How do we serve a trained model?”**

---

### 🔹 `main` — MLOps-Oriented Workflow (Current)

Purpose:

* Introduce MLflow for experiment tracking and model registry
* Prepare the system for CI/CD and automated deployments
* Keep inference logic clean and registry-agnostic

Includes:

* MLflow-tracked training pipeline
* Batch inference pipeline
* Online inference API

This branch answers:
**“How does this become production-ready?”**



## 🧭 High-Level System Flow

```
Raw Data
   ↓
Training Pipeline
   ↓
MLflow (experiment tracking & model registry)
   ↓
Batch Inference Pipeline
   ↓
Predictions (offline)

               ┌──────────────┐
               │  FastAPI API │
               │ (online use) │
               └───────▲──────┘
                       │
                 Loaded model
                 at startup
```

Key ideas:

* Training and serving are **decoupled**
* MLflow is used for **tracking and registry**
* Inference code loads models locally at runtime



## 🚀 Getting Started (High-Level)

1. **Explore ML experimentation**

   * Switch to `ml-baseline` branch

2. **Understand serving without MLOps**

   * Switch to `api-baseline` branch

3. **Run the full MLOps-style workflow**

   * Stay on `main` branch
   * Follow the documentation below



## 📚 Documentation Guide

Detailed documentation is intentionally split to keep concerns isolated.

* **DVC (data versioning)**
  → [docs/dvc.md](docs/dvc.md)

* **MLflow (training & tracking)**
  → [docs/mlflow.md](docs/mlflow.md)

* **Batch inference & Online API**
  → [docs/api.md](docs/api.md)

Each document focuses only on its responsibility.


## 🗂️ Repository Structure (Main Branch)

```
root
├── .dvc/              # DVC configuration
├── data/              # Raw data and inference inputs
├── docs/              # MLOps and API documentation
├── pipelines/         # Training & batch inference entry points
├── src/               # Core ML logic and API implementation
├── tests/             # API tests
├── outputs/           # Batch inference outputs
├── Dockerfile         # API container definition
├── requirements/      # Dependency separation (train / api)
└── README.md
```


## 🧪 Testing

API tests can be executed with:

```bash
pytest -v
```


## 🐳 Containerization

The online inference API is Dockerized for deployment and portability.
Refer to [docs/api.md](docs/api.md) for details.

---
