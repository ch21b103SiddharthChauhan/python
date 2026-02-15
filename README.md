# DA5402 – Assignment 1  
## Manual MLOps Challenge  

**Name:** Siddharth Chauhan  
**Roll Number:** CH21B103  

---

## Project Overview

This project implements a fully manual MLOps pipeline for a Predictive Maintenance system using the AI4I 2020 dataset.

The objective is to simulate the complete lifecycle of a production ML system without using automated MLOps tools such as MLflow, DVC, Airflow, Kubeflow, or Kubernetes.

The system includes:

- Manual data versioning  
- Configuration-driven training  
- Manual model registry  
- API deployment using FastAPI  
- Deployment logging  
- Smoke testing  
- Production monitoring  
- Manual retraining trigger  

---

## Environment Setup

It is recommended to use a virtual environment.

python -m venv venv


Activate it:
**Windows**
venv\Scripts\activate


**Mac/Linux**
source venv/bin/activate


### Install dependencies
pip install -r requirements.txt


---
## How to Run the Project

Follow the steps below in order.
---
### Step 1: Data Preparation

python src/data_prep.py

This will:

- Load the raw dataset  
- Perform preprocessing and encoding  
- Split the data chronologically (7000 train / 3000 test)  
- Save processed datasets  
- Update `manifest.txt`  

---

### Step 2: Train the Model

python src/train.py

This will:

- Load dataset paths from `config.yaml`  
- Train a RandomForest model  
- Evaluate accuracy  
- Save the model artifact  
- Log metadata including Git commit hash  

---

### Step 3: Deploy the Model

Start the API:

uvicorn src.inference:app --port 5000

Open in your browser:

http://127.0.0.1:5000/docs


Use the `/predict` endpoint to test predictions.

Each time the API starts, the deployed model is recorded in `deployment_log.csv`.

---

### Step 4: Run Smoke Tests

Ensure the API is running, then execute:

python src/test_api.py

This validates:

- API status code  
- Response structure  
- Prediction datatype  

---

### Step 5: Monitor Production Performance

Ensure the API is running, then execute:

python src/monitor.py

This will:

- Send Day-2 production data to the API  
- Compute production accuracy  
- Compare accuracy with threshold in `config.yaml`  
- Indicate whether retraining is required  

---

## Configuration Control

All paths and parameters are stored in:

config.yaml

No hardcoded dataset paths are used in training or deployment scripts.

---

## Dataset

AI4I 2020 Predictive Maintenance Dataset  
UCI Machine Learning Repository  

---

## Summary

This project demonstrates the complete lifecycle of a manual ML system:

Raw Data → Versioned Data → Training → Model Registry → Deployment → Monitoring → Retraining

It highlights the challenges and operational risks of managing ML systems without automated MLOps tools.


