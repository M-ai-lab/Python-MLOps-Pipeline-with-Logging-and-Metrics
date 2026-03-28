# MLOps Batch Pipeline for Signal Generation

## 📌 Overview

This project implements a minimal MLOps-style batch job in Python to process OHLCV data and generate trading signals. It demonstrates core MLOps principles such as reproducibility, observability, and containerized deployment.

---

## ⚙️ Key Features

* Config-driven execution using YAML
* Deterministic results using a fixed random seed
* Rolling mean computation on price data
* Binary signal generation
* Structured metrics output (JSON)
* Detailed logging for monitoring
* Dockerized for one-command execution

---

## 📂 Project Structure

```
├── run.py
├── config.yaml
├── data.csv
├── requirements.txt
├── Dockerfile
├── metrics.json
├── run.log
└── README.md
```

---

## 📥 Input Files

### config.yaml

```yaml
seed: 42
window: 5
version: "v1"
```

### data.csv

* Contains OHLCV data
* Only the **close** column is used

---

## 🚀 Execution

### ▶️ Run Locally

```bash
pip install -r requirements.txt

python run.py --input data.csv --config config.yaml --output metrics.json --log-file run.log
```

---

### 🐳 Run with Docker

#### Build Image

```bash
docker build -t mlops-task .
```

#### Run Container

```bash
docker run --rm mlops-task
```

---

## ⚙️ Processing Steps

1. Load and validate configuration
2. Load and validate dataset
3. Compute rolling mean on `close` using window
4. Generate signal:

   * 1 if close > rolling mean
   * 0 otherwise
5. Compute metrics:

   * rows_processed
   * signal_rate
   * latency_ms
6. Save metrics and logs

---

## 📊 Output

### metrics.json (Success)

```json
{
  "version": "v1",
  "rows_processed": 10000,
  "metric": "signal_rate",
  "value": 0.4990,
  "latency_ms": 127,
  "seed": 42,
  "status": "success"
}
```

### metrics.json (Error)

```json
{
  "version": "v1",
  "status": "error",
  "error_message": "Description of the issue"
}
```

---

## 📝 Logging

Logs are stored in `run.log` and include:

* Job start and end time
* Config validation
* Data loading details
* Processing steps
* Metrics summary
* Error messages (if any)

---

## ✅ MLOps Concepts Demonstrated

* **Reproducibility**: Controlled via config and seed
* **Observability**: Logging and structured metrics
* **Deployment**: Dockerized execution
* **Reliability**: Input validation and error handling

---

## 📌 Notes

* Metrics file is generated in both success and failure cases
* No hardcoded paths are used
* Designed for clarity and extensibility

---

## 👩‍💻 Author

Manjula Srividya
