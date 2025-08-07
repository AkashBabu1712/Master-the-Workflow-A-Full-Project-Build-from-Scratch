# 🧠 Machine Learning Project Documentation  
**Day 01: Environment Setup & GitHub Integration**

## 📦 Step-by-Step Workflow

### 1️⃣ Create GitHub Repository
- Go to GitHub and create a new repository (e.g., `ML-Project`)
- Add a `.gitignore` file (Python template recommended)
- Initialize with a README.md

### 2️⃣ Local Folder Setup
- Create a folder on your local drive with the same name as the repository
- Copy the folder path for terminal navigation

### 3️⃣ Launch VS Code via Anaconda Prompt
```bash
cd <path-to-your-folder>
code .
```
This opens the folder in VS Code.

### 4️⃣ Create Virtual Environment
In VS Code terminal:
```bash
conda create -p venv python=3.11.5 -y
conda activate venv/
```

### 5️⃣ Initialize Git & Link to GitHub
```bash
git init
echo "# ML Project" > README.md
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/AkashBabu1712/ML-Project.git
git push -u origin main
```

### 6️⃣ Sync Git Global Config (if needed)
```bash
git config --global user.name "Akash Babu"
git config --global user.email "kumar111aakash.in@gmail.com"
```

### 7️⃣ Create `setup.py` for Packaging
```python
from typing import List
from setuptools import find_packages, setup

HYPEN_E_DOT = '-e .'

def get_requirements(file_path: str) -> List[str]:
    '''
    Returns a list of requirements from the given file.
    '''
    with open(file_path) as file_obj:
        requirements = file_obj.readlines()
        requirements = [req.strip() for req in requirements]
        if HYPEN_E_DOT in requirements:
            requirements.remove(HYPEN_E_DOT)
    return requirements

setup(
    name='ML Project',
    version='0.0.1',
    author='Akash',
    author_email='kumar111aakash.in@gmail.com',
    packages=find_packages(),
    install_requires=get_requirements('requirements.txt')
)
```

### 8️⃣ Create `requirements.txt`
List all dependencies. Example:
```
numpy
pandas
scikit-learn
matplotlib
-e .
```

### 9️⃣ Create `src/` Directory
Inside your project folder:
- Create a folder named `src`
- Inside `src`, add an empty `__init__.py` file

### 🔟 Final Setup & Push
```bash
pip install -r requirements.txt
git add .
git status
git commit -m "setup"
git push -u origin main
```