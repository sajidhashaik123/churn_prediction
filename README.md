# Telco Customer Churn Prediction – End-to-End MLOps Platform

## 1. Project Overview

The **Telco Customer Churn Prediction – End-to-End MLOps Platform** is a machine learning project designed to predict whether a telecommunications customer is likely to discontinue their service.

The project demonstrates an end-to-end MLOps lifecycle, covering data ingestion, validation, preprocessing, model training, experiment tracking, model evaluation, model registration, deployment, inference, monitoring, and automation.

The platform integrates machine learning workflows with deployment and orchestration technologies to support reproducible, maintainable, and scalable model operations.

## 2. Project Objectives

- Develop a machine learning model to predict customer churn.
- Implement data ingestion and validation workflows.
- Perform reproducible data preprocessing.
- Track experiments and model performance using MLflow.
- Register and manage model versions.
- Implement model evaluation and quality gates.
- Automate model lifecycle management.
- Develop an API for model inference using FastAPI.
- Generate interactive API documentation using Swagger UI.
- Containerize the application using Docker.
- Deploy and manage the application using Kubernetes.
- Implement data drift, prediction drift, and concept drift analysis.
- Automate monitoring workflows using GitHub Actions.

## 3. Project Workflow

The project follows an integrated MLOps workflow:

1. Data ingestion
2. Data validation
3. Data preprocessing
4. Dataset preparation
5. Model training
6. Experiment tracking using MLflow
7. Model evaluation
8. Quality gate verification
9. Model registration
10. Model lifecycle management
11. Model inference
12. API development and performance monitoring
13. Drift analysis and monitoring automation
14. Docker containerization
15. Kubernetes deployment
16. GitHub Actions automation

## 4. System Architecture

The platform consists of the following major components:

| Component | Description |
|---|---|
| Data Pipeline | Loads and prepares customer data |
| Data Validation | Checks data quality and schema |
| Preprocessing | Transforms raw data into model-ready features |
| Model Training | Trains machine learning models |
| MLflow | Tracks experiments and manages model versions |
| Model Evaluation | Evaluates model performance |
| Quality Gate | Checks whether model metrics satisfy configured thresholds |
| Model Registry | Manages model versions and lifecycle stages |
| FastAPI | Provides model prediction endpoints |
| Swagger UI | Provides interactive API documentation |
| Docker | Packages the application and dependencies |
| Kubernetes | Manages container deployment |
| Monitoring | Analyzes model and data drift |
| GitHub Actions | Automates configured workflows |

## 5. Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn |
| Experiment Tracking | MLflow |
| API Development | FastAPI, Pydantic, Uvicorn |
| API Documentation | Swagger UI |
| Containerization | Docker |
| Container Orchestration | Kubernetes |
| Automation | GitHub Actions |
| Version Control | Git, GitHub |
| Environment Management | Python Virtual Environment |

## 6. Dataset

The project uses a Telco Customer Churn dataset containing customer information and service-related attributes.

The dataset supports the prediction of customer churn using information such as:

- Customer demographics
- Account information
- Service subscriptions
- Contract details
- Payment methods
- Monthly charges
- Total charges
- Churn status

**Target variable:** `Churn`

The target variable indicates whether a customer has discontinued the service.

## 7. Project Structure

The project is organized into modules to separate data processing, machine learning, API development, deployment, monitoring, and documentation.

```text
churn-prediction-full-project-files/
│
├── .github/
│   └── workflows/
│       ├── lab13_monitoring.yml
│       ├── lab13_runner_test.yml
│       └── lab8_ci.yml
│
├── api/
│   ├── main.py
│   ├── model_loader.py
│   ├── monitoring_logger.py
│   ├── preprocessing.py
│   └── schemas.py
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── splits/
│
├── deployment/
│   ├── model.pkl
│   ├── preprocessor.pkl
│   ├── model_metadata.json
│   └── deploy_production.py
│
├── docs/
├── k8s/
├── lab11_commands/
├── models/
├── notebooks/
├── pipelines/
├── reports/
├── src/
│   └── mlops_pipeline/
│
├── tests/
│
├── Dockerfile
├── .dockerignore
├── .gitignore
├── config.yaml
├── requirements.txt
├── requirements-api.txt
└── README.md
```

## 8. Installation and Setup

### Prerequisites

Install the following tools:

- Python 3.10 or later (use a version compatible with the project's dependencies)
- Git
- Docker Desktop
- Kubernetes and kubectl
- Visual Studio Code or another Python IDE

### Clone the Repository

```bash
git clone https://github.com/jnaneswar077/churn-prediction-mlops.git
```

Navigate to the project directory:

```bash
cd churn-prediction-mlops
```

### Create a Virtual Environment

Windows:

```powershell
python -m venv venv
```

Activate it:

```powershell
.\venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
python3 -m venv venv
source venv/bin/activate
```

### Install Dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Install API dependencies:

```bash
pip install -r requirements-api.txt
```

## 9. Data Processing and Model Training

The project includes scripts for data ingestion, validation, preprocessing, model training, and evaluation.

The main workflow scripts are organized under the project source directories.

Before training, ensure that the required dataset is available at the configured data path.

The project uses configuration settings from `config.yaml` to manage data paths, model parameters, and quality-gate requirements.

## 10. Experiment Tracking and Model Management

MLflow is used for experiment tracking and model management.

The workflow supports:

- Recording model parameters
- Tracking evaluation metrics
- Saving model artifacts
- Comparing experiment runs
- Registering trained models
- Managing model versions
- Supporting model lifecycle decisions

The configured model registry name is:

`Telco_Churn_Production_Model`

The quality gate uses recall with a configured minimum threshold of `0.70`.

A candidate model must satisfy the configured quality requirements before it can proceed through the applicable lifecycle and deployment steps.

## 11. Model Serving with FastAPI

The project includes a FastAPI application in the `api/` directory.

FastAPI provides an interface for sending customer information to the trained model and obtaining churn predictions.

The application uses the model and preprocessing artifacts stored in the `deployment/` directory.

Start the API from the project root:

```bash
python -m uvicorn api.main:app --host 127.0.0.1 --port 8000
```

### Swagger UI

After the API starts successfully, open:

`http://127.0.0.1:8000/docs`

Swagger UI provides interactive documentation for exploring and testing the available API endpoints.

Alternative API documentation:

`http://127.0.0.1:8000/redoc`

## 12. Docker Containerization

Docker is used to package the FastAPI application and its required dependencies into a container image.

The project includes:

- `Dockerfile`
- `requirements-api.txt`
- `.dockerignore`

Build the Docker image:

```bash
docker build -t churn-prediction-api:model-v1 .
```

Run the container:

```bash
docker run -p 8000:8000 churn-prediction-api:model-v1
```

Access Swagger UI:

`http://localhost:8000/docs`

Check running containers:

```bash
docker ps
```

## 13. Kubernetes Deployment

Kubernetes is used to manage the containerized API application.

The project contains Kubernetes deployment and service configuration files under the `k8s/` directory.

Check cluster connectivity:

```bash
kubectl cluster-info
```

View available nodes:

```bash
kubectl get nodes
```

Apply the deployment and service manifests using their actual filenames:

```bash
kubectl apply -f k8s/
```

Check deployments:

```bash
kubectl get deployments
```

Check pods:

```bash
kubectl get pods
```

Check services:

```bash
kubectl get services
```

The container image must be available to the Kubernetes cluster before the deployment can run successfully.

## 14. Monitoring and Drift Analysis

The project includes monitoring workflows for analyzing changes in incoming data and model predictions.

The monitoring components cover:

- Data drift analysis
- Prediction drift analysis
- Concept drift analysis
- Model performance monitoring
- API performance monitoring
- Prediction request history
- Monitoring-trigger decisions
- Conditional retraining workflows

The monitoring scripts are organized in the project and include:

- `12_data_drift.py`
- `12_prediction_drift.py`
- `12_concept_drift.py`
- `12_drift_analysis.py`
- `12_monitor_trigger.py`
- `12_retrain_model.py`

The combined drift analysis uses existing drift reports as inputs. The underlying monitoring scripts must refresh those reports before the combined analysis is run.

## 15. GitHub Actions Automation

GitHub Actions is used to automate configured project workflows.

The project includes workflow files such as:

```text
.github/workflows/
├── lab8_ci.yml
├── lab13_monitoring.yml
└── lab13_runner_test.yml
```

The Lab 13 workflow uses a self-hosted Windows runner.

It invokes the monitoring-trigger script, checks the generated monitoring report, and verifies Kubernetes deployment information.

**Environment requirement:** The current Lab 13 workflow contains machine-specific Windows directory references. Update both project-directory references in the workflow before executing it on another computer. The self-hosted runner, virtual environment, required dependencies, and Kubernetes context must be available.

## 16. Recorded Integration Results

The previously documented integration run reported the following:

- Candidate model version: `17`
- Candidate recall: `0.7219`
- Configured minimum recall: `0.70`
- Existing Production recall: approximately `0.7807`
- Candidate promotion decision: Rejected
- Production model version: `1`
- Deployment decision: Skipped

The candidate passed the minimum recall threshold but did not outperform the existing Production model under the documented lifecycle decision.

These values describe the recorded integration run and should not be interpreted as results from every subsequent execution.

## 17. Reproducibility and Configuration

The project uses configuration files, virtual environments, dependency lists, and version-controlled scripts to support reproducibility.

Important files include:

- `config.yaml` – project configuration
- `requirements.txt` – general Python dependencies
- `requirements-api.txt` – API dependencies
- `.gitignore` – Git exclusion rules
- `.dockerignore` – Docker build exclusions

Use the same compatible dependency versions and configuration when reproducing an experiment or deployment.

## 18. Future Improvements

- Improve model performance through hyperparameter optimization.
- Extend automated model retraining workflows.
- Improve monitoring visualization and reporting.
- Add more comprehensive API integration tests.
- Improve deployment portability across environments.
- Extend CI/CD automation.
- Add model explainability and feature-importance analysis.
- Improve production logging and alerting.

## 19. Conclusion

This project demonstrates an end-to-end MLOps platform for telecommunications customer churn prediction.

It combines machine learning, experiment tracking, model lifecycle management, API development, Docker containerization, Kubernetes orchestration, drift analysis, and workflow automation.

The platform demonstrates how machine learning models can be developed, evaluated, managed, served, and monitored through an organized MLOps workflow.



