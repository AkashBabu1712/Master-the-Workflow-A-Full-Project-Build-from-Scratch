# 🧠 Machine Learning Project Documentation  
**Day 03: Exploratory Data Analysis & Model Training**

## 📂 Components Created
- `components/data_analysis.py` – Handles EDA, visualizations, and insights
- `components/model_trainer.py` – Prepares data, trains models, and evaluates performance

---

## 📊 Student Performance Indicator – Project Lifecycle

### 🔹 ML Lifecycle Steps
1. Understanding the Problem Statement  
2. Data Collection  
3. Data Checks  
4. Exploratory Data Analysis (EDA)  
5. Data Preprocessing  
6. Model Training  
7. Model Evaluation  
8. Best Model Selection

---

## 🧩 Problem Statement
Analyze how student performance (math scores) is influenced by:
- Gender
- Ethnicity
- Parental education
- Lunch type
- Test preparation course

---

## 📥 Data Collection
- Source: [Kaggle Dataset](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams?datasetId=74977)
- Shape: 1000 rows × 8 columns

---

## 📋 Data Checks
Performed checks for:
- Missing values → None found  
- Duplicates → None found  
- Data types → Verified  
- Unique values → Counted  
- Descriptive statistics → Analyzed

---

## 📈 Exploratory Data Analysis (EDA)

### 🔸 Feature Engineering
- Added `total score` and `average` columns
- Identified students with full marks and low scores

### 🔸 Visualizations
- Histograms & KDE plots for score distributions
- Violin plots for subject-wise score spread
- Pie charts for categorical feature proportions
- Bar plots for bivariate analysis (gender, race, lunch, etc.)
- Box plots for outlier detection
- Pairplot for multivariate relationships

### 🔸 Key Insights
- Females outperform males overall; males excel in math  
- Standard lunch correlates with better performance  
- Parental education has mixed impact  
- Race groups A & B show lower scores  
- Test preparation course completion improves scores  
- Scores across subjects are positively correlated

---

## 🤖 Model Training

### 🔸 Target Variable
- `math_score`

### 🔸 Feature Transformation
```python
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.compose import ColumnTransformer

preprocessor = ColumnTransformer([
    ("OneHotEncoder", OneHotEncoder(), cat_features),
    ("StandardScaler", StandardScaler(), num_features)
])
X = preprocessor.fit_transform(X)
```

### 🔸 Models Evaluated
- Linear Regression
- Lasso, Ridge
- KNN
- Decision Tree
- Random Forest
- XGBoost
- CatBoost
- AdaBoost

### 🔸 Evaluation Metrics
```python
def evaluate_model(true, predicted):
    mae = mean_absolute_error(true, predicted)
    mse = mean_squared_error(true, predicted)
    rmse = np.sqrt(mse)
    r2 = r2_score(true, predicted)
    return mae, rmse, r2
```

### 🔸 Results Summary
- R² scores compared across models
- Linear Regression accuracy: ~XX% (based on your output)
- Visual comparison of actual vs predicted values
- Difference table for prediction errors

---

## ✅ Conclusion
- Lunch type, race/ethnicity, and parental education significantly influence performance  
- Females lead in overall scores; males in math  
- Test preparation course completion yields better results  
- Linear regression provides a baseline; ensemble models may offer improvements
