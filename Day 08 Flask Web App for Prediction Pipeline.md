# 🌐 Machine Learning Project Documentation  
**Day 08: Flask Web App for Prediction Pipeline**

## 📂 Files Created
- `app.py` – Flask application entry point  
- `templates/index.html` – Home page  
- `templates/home.html` – Prediction form  
- `src/pipeline/predict_pipeline.py` – Backend prediction logic

---

## 🚀 Purpose
To deploy a user-friendly web interface that allows users to input student data and receive predicted math scores using the trained ML model.

---

## 🧱 Flask App Structure

### 🔹 `app.py`

#### Key Routes:
- `/` → Renders `index.html`  
- `/predictdata` → Handles GET (form display) and POST (prediction)

#### Core Logic:
- Collects form data via `CustomData` class  
- Converts input to DataFrame  
- Passes data to `PredictPipeline` for preprocessing and prediction  
- Displays result on `home.html`

```python
@app.route('/predictdata', methods=['GET', 'POST'])
def predict_datapoint():
    ...
    data = CustomData(...)
    pred_df = data.get_data_as_data_frame()
    predict_pipeline = PredictPipeline()
    results = predict_pipeline.predict(pred_df)
    return render_template('home.html', results=results[0])
```

---

## 🖼️ HTML Templates

### 🔹 `index.html`
Simple welcome page:
```html
<h1>Welcome to the home page</h1>
```

### 🔹 `home.html`
Interactive form for user input:
- Gender, Ethnicity, Parental Education  
- Lunch Type, Test Preparation Course  
- Reading & Writing Scores  
- Submit button triggers prediction  
- Displays predicted math score

```html
<h2>THE prediction is {{results}}</h2>
```

> Note: Reading and writing scores are swapped in the form field names. You may want to correct that for clarity.

---

## 🧠 Prediction Pipeline

### 🔹 `predict_pipeline.py`

#### `CustomData` Class
- Converts user input into a pandas DataFrame

#### `PredictPipeline` Class
- Loads model and preprocessor from `artifacts/`  
- Transforms input data  
- Predicts math score  
- Returns result

```python
model = load_object("artifacts/model.pkl")
preprocessor = load_object("artifacts/preprocessor.pkl")
data_scaled = preprocessor.transform(features)
preds = model.predict(data_scaled)
```

---

## ✅ Output
- User inputs student details via form  
- Backend processes and predicts math score  
- Result displayed on the same page

---

## 📌 Deployment Notes
- Run locally using:
  ```bash
  python app.py
  ```
- Accessible at `http://localhost:5000/`  
- For production, consider using Gunicorn + Docker or deploying to platforms like Heroku or Azure
