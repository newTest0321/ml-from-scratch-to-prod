# 🌐 Inference & API

This document describes how **batch inference** and the **online inference API**
are executed in this project.

The API and inference pipelines reuse the same preprocessing and prediction logic
that was finalized during training.


## 📦 Batch Inference Pipeline

Batch inference is used for **offline predictions** on CSV inputs.

### ▶️ Run Batch Inference

```bash
python -m pipelines.inference
```

### What this pipeline does

* Loads the trained model and preprocessing artifacts
* Applies the same preprocessing steps used during training
* Runs predictions on the provided inference dataset
* Writes prediction results to disk

### Output location

```
outputs/predictions.json
```

### Generating sample input data

Sample inference input can be generated using:

```bash
python data/inference/generate_sample.py
```



## 🌐 Online Inference API

The project exposes a **FastAPI-based service** for real-time housing price
predictions.

### API Characteristics

* FastAPI REST service
* Request and response validation using Pydantic
* Shared preprocessing logic with training and batch inference
* Artifacts loaded once during application startup
* Structured file-based logging
* Automated API tests
* Docker-ready for deployment

### Available Endpoints

* `GET /health`
  Health check endpoint

* `POST /predict`
  Run housing price predictions on input features



## ▶️ Running the API Locally

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

### Access the API

* API base URL: [http://localhost:8000](http://localhost:8000)
* Swagger UI: [http://localhost:8000/docs](http://localhost:8000/docs)



## 🐳 Running the API with Docker

```bash
docker build -t housing-api .
docker run -p 8000:8000 housing-api
```


## 🧪 Running API Tests

```bash
pytest -v
```


## 🧭 Notes

* The API does **not** serve models directly from MLflow
* Model and preprocessing artifacts are loaded locally at startup

---