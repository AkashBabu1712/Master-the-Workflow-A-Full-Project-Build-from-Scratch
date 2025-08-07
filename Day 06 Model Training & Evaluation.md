# 🧠 Machine Learning Project Documentation  
**Day 06: Model Training & Evaluation**

## 📂 File Created
- `src/components/data_Model.py`

---

## 🎯 Purpose
This module trains multiple regression models, performs hyperparameter tuning using GridSearchCV, evaluates performance using R² score, and saves the best-performing model.

---

## 🧱 Structure Overview

### 🔹 `ModelTrainerConfig` (via `@dataclass`)
Stores path for saving the trained model:
```python
trained_model_file_path = os.path.join("artifacts", "model.pkl")
```

---

### 🔹 `ModelTrainer` Class

#### 🔸 `initiate_model_trainer(train_array, test_array)`
Main method that:
- Splits input arrays into features and target
- Defines a dictionary of models
- Specifies hyperparameter grids
- Evaluates models using `evaluate_models()` from `utils.py`
- Selects and saves the best model
- Returns R² score on test data

---

## 🤖 Models Used
| Model Name               | Library           |
|--------------------------|-------------------|
| Random Forest            | `sklearn.ensemble`  
| Decision Tree            | `sklearn.tree`  
| Gradient Boosting        | `sklearn.ensemble`  
| Linear Regression        | `sklearn.linear_model`  
| XGBoost                  | `xgboost`  
| CatBoost                 | `catboost`  
| AdaBoost                 | `sklearn.ensemble`  

---

## 🔧 Hyperparameter Tuning
Each model is tuned using a predefined grid. Example:

```python
"Random Forest": {
    'n_estimators': [8, 16, 32, 64, 128, 256]
}
"CatBoosting Regressor": {
    'depth': [6, 8, 10],
    'learning_rate': [0.01, 0.05, 0.1],
    'iterations': [30, 50, 100]
}
```

---

## 📊 Evaluation Logic

### 🔹 `evaluate_models()` (from `utils.py`)
- Performs GridSearchCV for each model  
- Fits best parameters  
- Evaluates using R² score  
- Returns a dictionary of model scores

### 🔹 Best Model Selection
```python
best_model_score = max(sorted(model_report.values()))
best_model_name = list(model_report.keys())[list(model_report.values()).index(best_model_score)]
```

If no model achieves R² > 0.6, a `CustomException` is raised.

---

## 💾 Model Persistence
Best model is saved using:
```python
save_object(file_path=trained_model_file_path, obj=best_model)
```

---

## ✅ Output
- Logs training progress and results  
- Returns R² score of the best model on test data  
- Saves model to `artifacts/model.pkl`
