# ☁️ Machine Learning Project Documentation  
**Day 09: Deployment to AWS Cloud via CI/CD Pipeline**

## 🎯 Goal
Deploy the Flask-based ML prediction app to AWS Elastic Beanstalk using GitHub-integrated CI/CD pipelines.

---

## 📁 Project Structure Updates

### 🔹 Create `.ebextensions/` Folder
This folder contains configuration files for Elastic Beanstalk.

#### 🔸 `python.config`
Specifies the WSGI entry point for the Flask app:

```yaml
option_settings:
  "aws:elasticbeanstalk:container:python":
    WSGIPath: application:application
```

> Note: This assumes your Flask app is defined in `application.py` with:
```python
application = app
```

---

## 📝 Rename `app.py` to `application.py`

Elastic Beanstalk expects the entry point to match the WSGI path. Update the file name and add:

```python
from flask import Flask
app = Flask(__name__)
application = app  # Required for AWS WSGI
```

---

## 🛠️ AWS Setup Steps

### 1️⃣ Create Elastic Beanstalk Application
- Go to AWS Management Console → Elastic Beanstalk  
- Create a new application (e.g., `ml-predictor-app`)  
- Choose platform: Python  
- Upload your zipped project folder or connect via GitHub

### 2️⃣ Set Up CI/CD Pipeline
- Go to AWS CodePipeline  
- Create a new pipeline  
- Source: GitHub repository (connect via OAuth)  
- Build provider: AWS CodeBuild (optional for preprocessing or testing)  
- Deploy provider: AWS Elastic Beanstalk  
- Select the application and environment created earlier

---

## 🔁 Deployment Flow

```mermaid
graph TD
A[GitHub Push] --> B[CodePipeline Trigger]
B --> C[CodeBuild (optional)]
C --> D[Elastic Beanstalk Deploy]
D --> E[Live Web App]
```

---

## ✅ Final Checklist

- [x] `.ebextensions/python.config` created  
- [x] `application.py` defined with `application = app`  
- [x] Requirements listed in `requirements.txt`  
- [x] GitHub repo connected to AWS CodePipeline  
- [x] Elastic Beanstalk environment running

---

## 🌐 Access
Once deployed, your app will be accessible via:
```
http://<your-environment-name>.elasticbeanstalk.com/
```