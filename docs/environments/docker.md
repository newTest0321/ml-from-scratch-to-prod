# 🐳 Docker-Based Environment

This document describes how to run the project using **Docker and Docker Compose**.

This setup runs:
- MLflow (tracking server + model registry)
- Training pipeline (one-shot container)
- Online inference API (FastAPI)


## 🧠 Docker Execution Model

In Docker mode:

- MLflow runs as a long-lived service
- Training runs as a **run-once container**
- The API runs as a long-lived service
- Training and inference communicate with MLflow via the Docker network
- Models are never baked into images

MLflow remains the **single source of truth** for models.


## 🚀 Step 1: Start MLflow & Run Training

Start MLflow and execute the training pipeline:

```bash
docker compose up mlflow train --build -d
```

### What this does

* Pulls MLflow and builds training images
* Starts the MLflow tracking server
* Runs the training pipeline as a one-shot container
* Logs experiments, metrics, and models to MLflow
* Registers the trained model and updates the `production` alias
* Leaves MLflow running after training completes



## 🔍 Step 2: Verify MLflow

Open the MLflow UI:

```
http://localhost:5000
```

Confirm:

* A new experiment run exists
* A model version is registered
* The `production` alias points to the latest version

If training needs to be re-run:

```bash
docker compose run --rm train
```



## 🌐 Step 3: Start the Inference API

Once a production model exists in MLflow, start the API:

```bash
docker compose up api --build -d
```

### What this does

* Builds the API image (if needed)
* Starts the FastAPI service
* Loads the `production` model from MLflow **once at startup**
* Exposes the inference API on port `8000`



## 🔎 Step 4: Access the API

* Health check:

  ```
  http://localhost:8000/health
  ```

* Swagger UI:

  ```
  http://localhost:8000/docs
  ```

* Prediction endpoint:

  ```
  http://localhost:8000/predict
  ```
  
  Executing a POST request to this endpoint with input data will return predictions.

  ```bash
  curl -X 'POST' \
    'http://127.0.0.1:8000/predict' \
    -H 'accept: application/json' \
    -H 'Content-Type: application/json' \
    -d '{
    "data": [
      {
        "households": 126,
        "housing_median_age": 41,
        "latitude": 37.88,
        "longitude": -122.23,
        "median_income": 8.3252,
        "ocean_proximity": "NEAR BAY",
        "population": 322,
        "total_bedrooms": 129,
        "total_rooms": 880
      }
    ]
  }'
  ```



## 🔁 Re-running Components

### Re-run training only

```bash
docker compose run --rm train
```

### Restart the API (after new model is promoted)

```bash
docker compose restart api
```

The API will load the updated `production` model on restart.



## 🧹 Cleanup

Stop all services:

```bash
docker compose down -v
```

---
