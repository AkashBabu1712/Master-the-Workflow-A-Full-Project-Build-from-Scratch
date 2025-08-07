# 🚀 Machine Learning Project Documentation  
**Day 11: End-to-End Deployment on AWS Cloud via CI/CD Pipeline**

## 🎯 Goal
Deploy a fully containerized ML application to AWS using a CI/CD pipeline powered by AWS CodePipeline, Docker, and supporting AWS services.

---

## 🧱 Step-by-Step Deployment Workflow

### 1️⃣ Define & Train the ML Model
- Use frameworks like TensorFlow, PyTorch, or scikit-learn  
- Save the trained model (e.g., `.pkl`, `.h5`)  
- Ensure all dependencies are listed in `requirements.txt`

---

### 2️⃣ Containerize the Application

#### 🔹 Create a Dockerfile

```dockerfile
# Base image
FROM python:3.8-slim-buster

# Set working directory
WORKDIR /app

# Copy project files
COPY . /app

# Install AWS CLI
RUN apt update -y && apt install awscli -y

# Install system dependencies and Python packages
RUN apt-get update && apt-get install ffmpeg libsm6 libxext6 unzip -y && pip install -r requirements.txt

# Run the Flask app
CMD ["python3", "app.py"]
```

> This Dockerfile ensures compatibility across environments and includes AWS CLI for integration tasks.

---

### 3️⃣ Build & Push Docker Image

```bash
# Build image
docker build -t ml-app-image .

# Tag and push to Amazon ECR
aws ecr create-repository --repository-name ml-app-image
docker tag ml-app-image:latest <your-ecr-uri>/ml-app-image:latest
docker push <your-ecr-uri>/ml-app-image:latest
```

---

### 4️⃣ Set Up AWS Services

| Service         | Purpose                          |
|----------------|----------------------------------|
| Amazon S3       | Store datasets or model artifacts |
| Amazon ECR      | Host Docker images                |
| AWS Lambda      | Optional serverless deployment    |
| Amazon ECS      | Container orchestration           |
| Amazon SageMaker| Model hosting (optional)          |
| AWS CloudWatch  | Monitoring and logging            |

---

### 5️⃣ Configure CI/CD Pipeline

#### 🔹 AWS CodePipeline Stages

| Stage     | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| Source    | Connect GitHub repo to pipeline                                             |
| Build     | Use AWS CodeBuild to build Docker image                                     |
| Test      | Run unit/integration tests (optional)                                       |
| Deploy    | Push image to ECS or trigger Lambda/SageMaker deployment                   |

---

### 6️⃣ Monitoring & Logging
- Use AWS CloudWatch for:
  - Application logs  
  - Performance metrics  
  - Error tracking

---

### 7️⃣ Scaling & Optimization
- Configure auto-scaling in ECS based on CPU/memory usage  
- Use spot instances or Fargate for cost efficiency  
- Optimize Docker layers for faster builds

---

### 8️⃣ Security Best Practices
- Use IAM roles with least privilege  
- Encrypt sensitive data (S3, EBS, communication)  
- Enable HTTPS and secure API endpoints

---

### 9️⃣ Versioning & Rollback
- Tag Docker images with version numbers  
- Maintain model version history  
- Use CodePipeline rollback triggers for failed deployments

---

### 🔟 Documentation & Continuous Improvement
- Document all configurations, secrets, and environment variables  
- Maintain a troubleshooting guide  
- Continuously monitor and refine pipeline performance
