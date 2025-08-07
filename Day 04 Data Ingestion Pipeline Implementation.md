# 🧠 Machine Learning Project Documentation  
**Day 04: Data Ingestion Pipeline Implementation**

## 📂 File Created
- `src/components/data_ingestion.py`

---

## ⚙️ Purpose
This module reads raw data, performs a train-test split, and saves the datasets to the `artifacts/` directory. It also triggers downstream components: data transformation and model training.

---

## 🧱 Structure Overview

### 🔹 `DataIngestionConfig` (via `@dataclass`)
Defines paths for:
- Raw data → `artifacts/data.csv`  
- Train data → `artifacts/train.csv`  
- Test data → `artifacts/test.csv`

### 🔹 `DataIngestion` Class
Handles:
- Reading raw CSV data (`stud.csv`)
- Logging progress
- Creating necessary directories
- Saving raw, train, and test datasets
- Returning file paths for downstream use

---

## 🧪 Code Summary

### 🔸 Configuration Setup
```python
@dataclass
class DataIngestionConfig:
    train_data_path: str = os.path.join('artifacts', "train.csv")
    test_data_path: str = os.path.join('artifacts', "test.csv")
    raw_data_path: str = os.path.join('artifacts', "data.csv")
```

### 🔸 Ingestion Logic
```python
df = pd.read_csv('notebook/data/stud.csv')
train_set, test_set = train_test_split(df, test_size=0.2, random_state=42)

df.to_csv(raw_data_path)
train_set.to_csv(train_data_path)
test_set.to_csv(test_data_path)
```

### 🔸 Logging & Exception Handling
- Logs each step using `logger.py`
- Wraps logic in try-except block using `CustomException`

---

## 🔄 Integration with Pipeline

### 🔹 Trigger Data Transformation
```python
data_transformation = DataTransformation()
train_arr, test_arr, _ = data_transformation.initiate_data_transformation(train_data, test_data)
```

### 🔹 Trigger Model Training
```python
model_trainer = ModelTrainer()
print(model_trainer.initiate_model_trainer(train_arr, test_arr))
```

---

## 📌 Notes
- All outputs are saved in the `artifacts/` folder for traceability  
- Modular design allows easy extension for validation sets or alternate data sources  
- Entry point (`__main__`) enables standalone execution and testing
