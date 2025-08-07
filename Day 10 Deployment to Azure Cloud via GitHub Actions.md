# ☁️ Machine Learning Project Documentation  
**Day 10: Deployment to Azure Cloud via GitHub Actions**

## 🎯 Goal
Automate deployment of your ML application to Azure Machine Learning using GitHub Actions and Docker.

---

## ✅ Prerequisites

| Requirement                     | Description                                                                 |
|----------------------------------|-----------------------------------------------------------------------------|
| Azure Account                   | Create one at [Azure Portal](https://portal.azure.com)                      |
| GitHub Repository               | Host your ML codebase                                                       |
| Azure Machine Learning Workspace| Set up via Azure Portal                                                     |
| Azure CLI                       | Install from [Azure CLI Download](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) |
| Docker                          | Install from [Docker Website](https://www.docker.com/)                      |

---

## 🧱 Step-by-Step Workflow

### 1️⃣ Set Up Azure ML Workspace
- Go to Azure Portal  
- Create a new Machine Learning Workspace  
- Note down:
  - Subscription ID  
  - Resource Group  
  - Workspace Name

---

### 2️⃣ Add Azure Credentials to GitHub
In your GitHub repository:
- Go to `Settings` → `Secrets` → `New Repository Secret`
- Add the following secrets:
  - `AZURE_SUBSCRIPTION_ID`  
  - `AZURE_RESOURCE_GROUP`  
  - `AZURE_WORKSPACE_NAME`  
  - `AZURE_MACHINELEARNING_KEY`  
  - `AZURE_CREDENTIALS` (JSON format for `azure/login@v1`)

---

### 3️⃣ Configure GitHub Actions Workflow

Create the file:  
`.github/workflows/azure-ml-deploy.yml`

```yaml
name: Azure ML Deployment

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.8

      - name: Install Dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Azure Login
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Build Docker Image
        run: |
          docker build -t your-docker-image-name .

      - name: Push Docker Image to Azure Container Registry
        run: |
          az acr login --name your-acr-name
          docker tag your-docker-image-name your-acr-name.azurecr.io/your-docker-image-name:latest
          docker push your-acr-name.azurecr.io/your-docker-image-name:latest

      - name: Deploy to Azure ML
        run: |
          az ml model deploy -n your-deployment-name \
            --image your-acr-name.azurecr.io/your-docker-image-name:latest \
            --cpu 1 --memory 1 \
            -f your-inference-config-file.yml
```

> Replace placeholders like `your-docker-image-name`, `your-acr-name`, `your-deployment-name`, and `your-inference-config-file.yml` with actual values.

---

### 4️⃣ Commit & Push
```bash
git add .
git commit -m "Add Azure ML deployment workflow"
git push origin main
```

---

### 5️⃣ Monitor Deployment
- Go to the `Actions` tab in your GitHub repository  
- Watch the workflow execute  
- If successful, your ML app will be deployed to Azure ML

---

## 📌 Notes
- Ensure your Dockerfile and inference config are correctly set up  
- You can customize CPU/memory allocation in the deployment step  
- For rollback or monitoring, use Azure ML Studio or CLI
