# ML from Scratch to Production

An end-to-end **Machine Learning engineering project** that demonstrates how a
model evolves from experimentation to **production-ready training pipelines,
batch inference, and an online inference API**.

The project uses the **California Housing dataset** as a reference use case and
focuses on building a **clean, reproducible, and deployable ML system** with
clear separation between modeling, pipelines, and serving.



## 🎯 What This Repository Represents

* Finalized ML pipelines (training & batch inference)
* A production-ready **FastAPI online inference service**
* Automated tests for the API
* Dockerized inference service

Detailed ML experimentation and modeling rationale are **documented separately**
and referenced below.



## 🧠 Machine Learning (Summary)

* Multiple model families were evaluated during experimentation
* Feature engineering was validated across models
* **Gradient Boosting (`HistGradientBoostingRegressor`)** achieved the best
  generalization performance
* This model was selected as the **production baseline**
* Only the finalized model and required preprocessing logic were migrated to
  Python pipelines

📘 **Detailed ML reasoning, experiments, and decisions** are documented here:

* `docs/` (step-by-step ML design)
* `notebooks/` (experimentation history)
* `ml-baseline` branch (ML-only checkpoint)



## 🗂️ Repository Structure (Main Branch)

```
root
├── artifacts/
│   ├── experiments/         # Historical experiment outputs
│   └── production/          # Deployment-ready ML artifacts
├── data/
│   ├── raw/                 # Original dataset
│   └── inference/           # Inference inputs & generators
├── docs/                    # ML design & decision records
├── notebooks/               # Experimentation history
├── pipelines/               # Training & batch inference entry points
├── src/                     # Production ML & API code
├── tests/                   # API tests
├── outputs/                 # Batch inference outputs
├── logs/                    # Training, inference & API logs
├── Dockerfile               # Inference service containerization
├── requirements/            # Dependency split (base / train / api)
└── README.md
```



## ⚙️ ML Pipelines (Completed)

### Training Pipeline

```bash
python -m pipelines.train
```

* Loads raw dataset
* Applies preprocessing and feature engineering
* Trains the final Gradient Boosting model
* Evaluates performance
* Saves production artifacts

Artifacts are written to:

```
artifacts/production/
```



### Batch Inference Pipeline

```bash
python -m pipelines.inference
```

* Loads production artifacts
* Applies identical preprocessing as training
* Runs predictions on inference input data

Outputs are written to:

```
outputs/predictions.json
```

Sample inference data can be generated using:

```bash
python data/inference/generate_sample.py
```



## 🌐 Online Inference API (Current Focus)

The system exposes a **FastAPI-based online inference service** for real-time
housing price predictions.

### API Characteristics

* FastAPI REST service
* Request/response validation using Pydantic
* Artifact loading via FastAPI lifespan events
* Shared preprocessing logic with training & batch inference
* Structured file-based logging
* Automated API tests
* Dockerized for deployment

### Available Endpoints

* `GET /health` — health check
* `POST /predict` — run housing price predictions



## ▶️ Running the API Locally (Python Environment)

### 1️⃣ Create and activate a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 2️⃣ Install API dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements/api.txt
```

### 3️⃣ Set Python path

```bash
export PYTHONPATH=$(pwd)/src
```

### 4️⃣ Start the API server

```bash
uvicorn api.main:app --reload
```

* API: [http://localhost:8000](http://localhost:8000)
* Swagger UI: [http://localhost:8000/docs](http://localhost:8000/docs)



## 🐳 Running the API with Docker

```bash
docker build -t housing-api .
docker run -p 8000:8000 housing-api
```



## 🧪 Running Tests

```bash
pytest -v
```

---
