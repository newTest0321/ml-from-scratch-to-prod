# ML from Scratch To Production

An end-to-end Machine Learning and MLOps project that demonstrates how to design,
train, validate, and operationalize a ml model using **industry-standard,
sequential ML engineering practices** and eventually deploy to production by implementing a full **MLOps pipeline**.

The project uses the California Housing dataset as a reference use case while
focusing on building a **reproducible and production-ready ML system**.

## 🎯 Project Objective

The objective of this project is to:

- Engineer a regression model **from scratch**
- Follow a **structured ML lifecycle** from data understanding to model validation
- Establish a **validated baseline model**
- Transition the solution into a **full MLOps workflow** using tools such as
  MLflow, data versioning, and automated pipelines

---

## 🧠 Machine Learning Phase (Completed)

The ML phase was implemented using a **progressive and evidence-driven approach**,
where each step informed the next.

### 1️⃣ Problem Framing & Data Understanding
- Clear definition of the prediction target (`median_house_value`)
- Dataset and feature analysis
- Identification of feature types and constraints

### 2️⃣ Baseline Modeling
- Linear Regression
- Ridge Regression
- Used to diagnose bias and scaling behavior

### 3️⃣ Non-Linear Modeling
- Decision Trees (unconstrained & constrained)
- Random Forest for variance control and baseline non-linear performance

### 4️⃣ Feature Engineering
- Domain-driven ratio features:
  - Rooms per household
  - Bedrooms per room
  - Population per household
- Evaluated impact systematically across models

### 5️⃣ Advanced Modeling
- Gradient Boosting using `HistGradientBoostingRegressor`
- Selected to reduce bias after Random Forest performance plateaued

### 6️⃣ Model Validation
- Hold-out test evaluation
- 5-fold cross-validation
- Stability assessed using RMSE and R²

👉 **Gradient Boosting with engineered features is selected as the current ML baseline.**

---

## 📊 Current Best Model

| Model | Test RMSE (≈) | CV RMSE (≈) | Notes |
|------|---------------|------------|------|
| Random Forest | ~49k | ~49k | Stable non-linear baseline |
| Gradient Boosting | **~45.5k** | **~46.5k** | Lower bias, improved accuracy |

Cross-validation confirms consistent generalization across data splits.

---

## 🧪 Repository Structure

```
mlops-house-price-prediction
├── artifacts/              # Trained models and evaluation metrics
├── data/                   # Raw and processed datasets
├── notebooks/              # ML experimentation and analysis
├── docs/                   # ML and MLOps decision documentation
├── src/                    # Production ML code (WIP)
├── pipelines/              # Training and inference pipelines (planned)
├── requirements.txt
└── README.md
```

---

## 📄 Documentation Philosophy

- **Notebooks** → experimentation and exploration
- **Docs** → reasoning, design choices, and conclusions
- **Artifacts** → reproducible model outputs and metrics
- **Source code** → reusable and production-ready ML components

---

## 🚀 MLOps Phase (In Progress)

The next phase focuses on operationalizing the validated ML model:

- MLflow for experiment tracking and model registry
- Data and artifact versioning
- Reproducible training pipelines
- Model packaging and deployment
- Monitoring and retraining strategies

The ML phase serves as a **stable foundation** for these MLOps components.

---

## 🧩 Design Principles

- Sequential ML development (baseline → validation → improvement)
- Explicit separation of experimentation and production code
- Reproducibility and traceability at every stage
- Model selection based on validated evidence

---

## 📌 Summary

This repository demonstrates how to engineer an ML model from scratch using
best practices and then extend it into a full MLOps system suitable for
production deployment.

