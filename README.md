# 📦 DB2 → Oracle Migration Validator

Enterprise-grade migration validation framework for comparing **DB2 and
Oracle** tables across environments (DEV / SIT / UAT).

------------------------------------------------------------------------

## 🚀 Features

-   Multi-environment support (dev / sit / uat)
-   Separate config files per environment
-   Row count validation
-   Hash-based data comparison
-   Batch processing (optimized for 1M+ rows)
-   Parallel execution
-   FastAPI REST API with Swagger UI
-   Streamlit dashboard
-   Docker & Kubernetes ready

------------------------------------------------------------------------

## 🏗 Project Structure

    db-migration-validator/
    │
    ├── app/
    │   ├── main.py
    │   ├── config_loader.py
    │   ├── db/
    │   ├── services/
    │   ├── utils/
    │
    ├── config/
    │   ├── config-dev.yaml
    │   ├── config-sit.yaml
    │   ├── config-uat.yaml
    │
    ├── dashboard/
    │   ├── streamlit_app.py
    │
    ├── Dockerfile
    ├── docker-compose.yml
    ├── requirements.txt
    └── README.md

------------------------------------------------------------------------

## ⚙ Environment Configuration

Each environment has its own config file:

-   config/config-dev.yaml
-   config/config-sit.yaml
-   config/config-uat.yaml

Switch environment using:

### Windows

    set APP_ENV=dev

### Linux / Mac

    export APP_ENV=dev

Available values: - dev - sit - uat

------------------------------------------------------------------------

## 🖥 Run Locally

### 1️⃣ Create Virtual Environment

Windows:

    python -m venv venv
    venv\Scripts\activate

Linux / Mac:

    python3 -m venv venv
    source venv/bin/activate

### 2️⃣ Install Dependencies

    pip install -r requirements.txt

### 3️⃣ Start API

    uvicorn app.main:app --reload

API URL:

    http://localhost:8000

Swagger UI:

    http://localhost:8000/docs

------------------------------------------------------------------------

## 📊 Run Streamlit Dashboard

    streamlit run dashboard/streamlit_app.py

Dashboard URL:

    http://localhost:8501

------------------------------------------------------------------------

## 🐳 Run Using Docker

### Build Image

    docker build -t db-validator .

### Run Container

    docker run -p 8000:8000 -e APP_ENV=sit db-validator

------------------------------------------------------------------------

## ☁ Kubernetes Deployment

In deployment YAML:

    env:
      - name: APP_ENV
        value: "uat"

Deploy:

    kubectl apply -f k8s-deployment.yaml

------------------------------------------------------------------------

## 🔍 API Endpoints

### Health Check

GET /health

### Validate Table

POST /validate/{table}

Example: POST /validate/EMPLOYEE

Response:

    {
      "table": "EMPLOYEE",
      "total_rows": 1000000,
      "mismatches": 0,
      "status": "PASS"
    }

------------------------------------------------------------------------

## ⚡ Performance Tuning (1M+ Rows)

Recommended: - Ensure table has Primary Key - Add index on comparison
columns - Increase batch size if memory allows - Tune threads based on
CPU cores

Example:

    validation:
      batch_size: 20000
      threads: 6

------------------------------------------------------------------------

## 🔐 Production Recommendations

-   Use Kubernetes Secrets for passwords
-   Remove plaintext passwords from YAML
-   Use connection pooling
-   Add audit table logging
-   Add PK-based delta comparison
-   Integrate Vault for credentials

------------------------------------------------------------------------

Built for enterprise-grade DB migration validation.
