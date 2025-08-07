# 🧠 Machine Learning Project Documentation  
**Day 05: Data Transformation & Utility Functions**

## 📂 Files Created
- `src/components/data_transformation.py` – Handles preprocessing pipeline
- `src/pipeline/utils.py` – Contains reusable utility functions

---

## 🔄 Data Transformation Pipeline

### 📌 Purpose
Transforms raw input features using:
- Imputation for missing values  
- Encoding for categorical variables  
- Scaling for numerical features  
- Combines transformed features with target variable  
- Saves the preprocessing object for future inference

---

### ⚙️ `DataTransformationConfig`
Stores path for saving the preprocessor object:
```python
preprocessor_obj_file_path = os.path.join('artifacts', "preprocessor.pkl")
```

---

### 🧪 `get_data_transformer_object()`
Returns a `ColumnTransformer` combining:
- 🔹 Numerical Pipeline:
  - Imputation: median
  - Scaling: StandardScaler
- 🔹 Categorical Pipeline:
  - Imputation: most frequent
  - Encoding: OneHotEncoder
  - Scaling: StandardScaler (without mean)

```python
preprocessor = ColumnTransformer([
    ("num_pipeline", num_pipeline, numerical_columns),
    ("cat_pipeline", cat_pipeline, categorical_columns)
])
```

---

### 🚀 `initiate_data_transformation(train_path, test_path)`
- Reads train/test CSVs  
- Separates input and target features  
- Applies transformation  
- Combines transformed arrays with target  
- Saves preprocessor using `save_object()`  
- Returns transformed arrays and preprocessor path

---

## 🛠️ Utility Functions (`utils.py`)

### 🔹 `save_object(file_path, obj)`
Serializes and saves any Python object using `pickle`.

### 🔹 `evaluate_models(X_train, y_train, X_test, y_test, models, param)`
- Performs GridSearchCV for each model  
- Fits best parameters  
- Evaluates using R² score  
- Returns a dictionary of model performance

```python
report[model_name] = test_model_score
```

### 🔹 `load_object(file_path)`
Loads a serialized object from disk.

---

## ✅ Highlights
- Modular design enables plug-and-play preprocessing  
- Uses `@dataclass` for clean config management  
- Logging and exception handling ensure traceability  
- Utility functions support model evaluation and object persistence
