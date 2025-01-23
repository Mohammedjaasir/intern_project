
# Predictive Analysis for Manufacturing Operations

This project involves building a RESTful API for predicting machine downtime or production defects using manufacturing data. The API provides endpoints for uploading data, training a machine learning model, and making predictions.

---

## Features

1. **Data Upload Endpoint**:
   - Allows users to upload a CSV file containing manufacturing data.

2. **Training Endpoint**:
   - Trains a supervised ML model (e.g., Decision Tree) on the uploaded data.
   - Returns performance metrics (e.g., accuracy, F1-score).

3. **Prediction Endpoint**:
   - Accepts JSON input (e.g., `{" Air Temperature": 80, "Torque [Nm]": 120}`).
   - Returns predictions in JSON format (e.g., `{ "Downtime": "Yes", "Confidence": 0.85 }`).

---

## Setup Instructions

### Prerequisites

- Python 3.7+
- Libraries: Flask, Flask-RESTful, scikit-learn, pandas

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/manufacturing-api.git
   cd manufacturing-api
   ```

2. Install dependencies:
   ```bash
   pip install flask scikit-learn flask-restful pandas
   ```

3. Launch the API:
   ```bash
   python app.py
   ```

4. The API will run locally at `http://127.0.0.1:5000`.

---

## API Endpoints

### 1. Upload Data

**URL:** `POST /upload`

**Description:** Upload a CSV file containing manufacturing data.

**Request:**
```
dataset = pd.read_csv('/content/predictive_maintenance.csv')
print(dataset.head(7))
```

**Response:**
```json
{
  "message": "File uploaded successfully",
  "data_sample": {
      Accuracy: 0.9525
      F1-score: 0.2748091603053435
      Returned F1-score: 0.2748091603053435
  }
}
```

---

### 2. Train Model

**URL:** `POST /train`

**Description:** Train a machine learning model on the uploaded dataset.

**Request:**
```bash
POST /train
```

**Response:**
```json
{
  "message": "Model trained successfully",
  "accuracy": 0.85
}
```

---

### 3. Predict

**URL:** `POST /predict`

**Description:** Predict machine downtime based on input parameters.

**Request:**
```json
{
  "Air Temperature": 80,
  "Torque [Nm]": 120
}
```

**Response:**
```json
{
  "Downtime": "Yes",
  "Confidence": 0.92
}
```

---

## Example API Testing

You can test the API using Postman or cURL.

### Using cURL

1. Upload Data:
   ```bash
   curl -X POST -F "file=@manufacturing_data.csv" http://127.0.0.1:5000/upload
   ```

2. Train Model:
   ```bash
   curl -X POST http://127.0.0.1:5000/train
   ```

3. Predict:
   ```bash
   curl -X POST -H "Content-Type: application/json" -d '{"Temperature": 80, "Run_Time": 120}' http://127.0.0.1:5000/predict
   ```

### Using Postman

- **Upload Data**:
  1. Select `POST` method.
  2. URL: `http://127.0.0.1:5000/upload`
  3. Go to the `Body` tab -> `form-data` -> Add key `file` and select a CSV file.

- **Train Model**:
  1. Select `POST` method.
  2. URL: `http://127.0.0.1:5000/train`

- **Predict**:
  1. Select `POST` method.
  2. URL: `http://127.0.0.1:5000/predict`
  3. Go to the `Body` tab -> `raw` -> Paste JSON input (e.g., `{ "Temperature": 80, "Run_Time": 120 }`).

---

## Dataset Example

| Air temp[K] | Rotational speed[rmp] | Torque [Nm]| Target |
|------------|-------------|----------|---------------|
| 1          | 80          | 100      | 0             |
| 2          | 90          | 120      | 1             |
| 3          | 85          | 110      | 0             |

---

## License

This project is open-source and available under the MIT License
