# API Design & Inference Flow

## Model loading strategy

The model is loaded once during application startup using FastAPI's
`lifespan` mechanism and stored in `app.state`.

This avoids:
- Loading the model per request
- Circular imports between `main.py` and routes
- Global mutable state

## Request flow

1. Request received
2. Input validated with Pydantic
3. Raw input converted to DataFrame
4. `model.predict(df)` executed
5. Predictions returned

## Why not import the model directly?

Importing the model from `main.py` inside routes causes partial
initialization and circular dependency issues.

Using `app.state` is the recommended FastAPI pattern for shared resources.