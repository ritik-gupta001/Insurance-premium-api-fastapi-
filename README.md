# Insurance Premium API (FastAPI)

This project provides a RESTful API for predicting insurance premium categories using a machine learning model. Built with [FastAPI](https://fastapi.tiangolo.com/), it allows users to submit information such as age, income, city, occupation, and lifestyle habits, and receive a prediction for their likely insurance premium category (e.g., Low, Medium, High), along with confidence scores.

## Features

- **/predict**: Accepts user data and returns the predicted insurance premium category with probabilities.
- **/health**: Health check endpoint for the API and model.
- Automatic calculation of features like BMI, lifestyle risk, and city tier based on input.
- Built with FastAPI for performance and easy API documentation.
- Dockerized for easy deployment.

## API Endpoints

### `POST /predict`

Predict the insurance premium category for a user.

**Request Body Example:**
```json
{
  "age": 35,
  "weight": 70,
  "height": 1.75,
  "income_lpa": 12,
  "smoker": false,
  "city": "Delhi",
  "occupation": "private_job"
}
```

**Response Example:**
```json
{
  "predicted_category": "Medium",
  "confidence": 0.81,
  "class_probabilities": {
    "Low": 0.09,
    "Medium": 0.81,
    "High": 0.10
  }
}
```

### `GET /health`

Returns API and model health status.

**Response Example:**
```json
{
  "status": "OK",
  "version": "1.0.0",
  "model_loaded": true
}
```

## How It Works

The API accepts user data and automatically computes:
- **BMI**: from weight and height
- **Lifestyle risk**: based on BMI and smoker status
- **Age group**: binned from age
- **City tier**: mapped from city name

A pre-trained machine learning model (scikit-learn) is used for prediction.

## Getting Started

### Requirements

- Python 3.11+
- [pip](https://pip.pypa.io/)
- [Docker](https://www.docker.com/) (optional, for containerized deployment)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/ritik-gupta001/Insurance-premium-api-fastapi-.git
   cd Insurance-premium-api-fastapi-
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the API:
   ```bash
   uvicorn INSURANCE\ PREMIUM\ PREDICTION.app:app --reload
   ```

   The API will be available at `http://localhost:8000`.

#### Using Docker

To build and run the API in a Docker container:

```bash
docker build -t insurance-premium-api .
docker run -p 8000:8000 insurance-premium-api
```

## File Structure

- `INSURANCE PREMIUM PREDICTION/app.py`: Main FastAPI app with endpoints.
- `Model/predict.py`: Model loading and prediction logic.
- `Schema/user_input.py`: Request validation and feature engineering.
- `Schema/prediction_response.py`: Prediction response schema.
- `config/city_tier.py`: City tier mapping.

## Example Usage

Test the API locally using [httpie](https://httpie.io/):

```bash
http POST http://localhost:8000/predict age=30 weight=68 height=1.70 income_lpa=10 smoker:=false city="Mumbai" occupation="private_job"
```

## License

This project is for educational/demo purposes. Please add a license file for production use.

---

**Author:** [ritik-gupta001](https://github.com/ritik-gupta001)
