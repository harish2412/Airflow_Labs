# Airflow Lab 2 – Random Forest on Breast Cancer with Flask Status API

This lab trains a *RandomForestClassifier* on the classic *Breast Cancer Wisconsin (Diagnostic)* dataset, logs evaluation metrics, saves the trained model, triggers an email alert, and starts a *Flask API* to show DAG success or failure after execution.

---

## What It Does

1. **Loads dataset** using `load_breast_cancer()` from scikit-learn  
2. **Splits data** into training and testing sets (80/20 stratified)  
3. **Trains** a Random Forest model using `GridSearchCV` for hyperparameter tuning  
4. **Logs metrics** (Cross-validation and test accuracy)  
5. **Saves trained model** to `dags/model/model.sav`  
6. **Sends email notification** via Gmail SMTP after successful run  
7. **Triggers Flask DAG** (`Airflow_Lab2_Flask`) to display pipeline statu.

---
## Changes in This Lab Assignment

1. Replaced the **advertising.csv** dataset with the **Breast Cancer Wisconsin (Diagnostic)** dataset.
2. Replaced the **Logistic Regression** model with a **Random Forest Classifier** trained via **GridSearchCV** for hyperparameter tuning.  
3. Removed all **scaling and column transformers** (`MinMaxScaler`, `StandardScaler`, `make_column_transformer`) since Random Forest does not require feature scaling.  
4. Implemented a **stratified train/test split** (80/20) using `train_test_split(..., stratify=y, random_state=42)` to ensure balanced class distribution.  
5. Updated `load_data()` to return data directly from scikit-learn instead of reading a CSV file, eliminating the need for file path handling.  
6. Modified `data_preprocessing()` to return `(X_train, X_test, y_train, y_test)` tuples directly instead of saving intermediate pickle files.  
7. Enhanced `build_model()` to log the **best CV accuracy**, save the tuned Random Forest model to `dags/model/model.sav`, and print detailed training results.  
8. Updated `load_model()` to load the new Random Forest model, display its **test accuracy**.
9. Added print statements and log outputs to improve **traceability** of data loading, model training, and evaluation stages in Airflow task logs.  


---
