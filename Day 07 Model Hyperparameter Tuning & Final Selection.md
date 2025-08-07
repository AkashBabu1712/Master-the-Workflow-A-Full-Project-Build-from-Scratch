# 🧠 Machine Learning Project Documentation  
**Day 07: Model Hyperparameter Tuning & Final Selection**

## 📂 File Updated
- `src/components/model_trainer.py`

---

## 🎯 Purpose
This module performs:
- Training of multiple regression models  
- Hyperparameter tuning using GridSearchCV  
- Evaluation using R² score  
- Selection and saving of the best-performing model

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
Performs the following steps:
1. Splits input arrays into features and target
2. Defines a dictionary of models
3. Specifies hyperparameter grids
4. Evaluates models using `evaluate_models()` from `utils.py`
5. Selects and saves the best model
6. Returns R² score on test data

---

## 🤖 Models & Hyperparameters

| Model Name               | Key Parameters Tuned |
|--------------------------|----------------------|
| Decision Tree            | `criterion`          |
| Random Forest            | `n_estimators`       |
| Gradient Boosting        | `learning_rate`, `subsample`, `n_estimators` |
| Linear Regression        | —                    |
| XGBoost                  | `learning_rate`, `n_estimators` |
| CatBoost                 | `depth`, `learning_rate`, `iterations` |
| AdaBoost                 | `learning_rate`, `n_estimators` |

> Note: Some parameters are commented out for future experimentation.

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
best_model = models[best_model_name]
```

If no model achieves R² > 0.6, a `CustomException` is raised.

---

## 💾 Model Persistence
Best model is saved using:
```python
save_object(file_path=self.model_trainer_config.trained_model_file_path, obj=best_model)
```

---

## ✅ Output
- Logs training progress and results  
- Returns R² score of the best model on test data  
- Saves model to `artifacts/model.pkl`  
- Enables future prediction via `predict_pipeline.py`
