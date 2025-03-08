# End-To-End-ML-Pipeline-With-MLOps

## Overview
This project demonstrates how to build an end-to-end machine learning pipeline using **DVC (Data Version Control)** for data and model versioning, and **MLflow** for experiment tracking. The pipeline trains a **Random Forest Classifier** on the **Pima Indians Diabetes Dataset**, following structured stages for **data preprocessing, model training, and evaluation**.

---

## Key Features
### 🔹 Data Version Control (DVC)
- Tracks and versions datasets, models, and pipeline stages to ensure reproducibility.
- Automates re-execution of pipeline stages when dependencies change.
- Supports remote data storage (e.g., **DagsHub, S3**).

### 🔹 Experiment Tracking with MLflow
- Logs hyperparameters (e.g., `n_estimators`, `max_depth`) and performance metrics.
- Tracks multiple experiment runs for easy comparison.
- Stores model artifacts for future reference.

---

## 🚀 Pipeline Stages
### 1️⃣ **Preprocessing** (`src/preprocess.py`)
- Reads raw dataset (`data/raw/data.csv`).
- Cleans and preprocesses data.
- Saves processed data to `data/processed/data.csv`.

```sh
dvc stage add -n preprocess \
  -p preprocess.input,preprocess.output \
  -d src/preprocess.py -d data/raw/data.csv \
  -o data/processed/data.csv \
  python src/preprocess.py
```

### 2️⃣ **Training** (`src/train.py`)
- Trains a **Random Forest Classifier**.
- Saves model as `models/random_forest.pkl`.
- Logs metrics and parameters in MLflow.

```sh
dvc stage add -n train \
  -p train.data,train.model,train.random_state,train.n_estimators,train.max_depth \
  -d src/train.py -d data/raw/data.csv \
  -o models/model.pkl \
  python src/train.py
```

### 3️⃣ **Evaluation** (`src/evaluate.py`)
- Loads trained model.
- Evaluates model performance (e.g., accuracy).
- Logs results to MLflow.

```sh
dvc stage add -n evaluate \
  -d src/evaluate.py -d models/model.pkl -d data/raw/data.csv \
  python src/evaluate.py
```

---

## 🎯 Goals
✅ **Reproducibility**: DVC ensures the same data, parameters, and code generate consistent results.
✅ **Experimentation**: MLflow allows easy tracking and comparison of different models.
✅ **Collaboration**: DVC and MLflow facilitate seamless teamwork.

---

## 🔧 Technology Stack
- **Python**: Core language for data processing, model training, and evaluation.
- **DVC**: Data versioning and pipeline automation.
- **MLflow**: Experiment tracking and model management.
- **Scikit-learn**: Machine learning library for training models.

---

## 📌 Use Cases
- **Data Science Teams**: Organize and track datasets, models, and experiments.
- **Machine Learning Research**: Iterate over different experiments and optimize models.
- **Enterprise AI Projects**: Maintain version control for scalable ML workflows.

---

## 📖 How to Use
1. **Clone the repository**
   ```sh
   git clone <repo_url>
   cd <repo_folder>
   ```
2. **Install dependencies**
   ```sh
   pip install -r requirements.txt
   ```
3. **Run the pipeline**
   ```sh
   dvc repro
   ```
4. **Track experiments**
   ```sh
   mlflow ui
   ```

---


## 📢 Contributing
Feel free to open issues or pull requests for improvements!

🚀 Happy Coding! 🎯

