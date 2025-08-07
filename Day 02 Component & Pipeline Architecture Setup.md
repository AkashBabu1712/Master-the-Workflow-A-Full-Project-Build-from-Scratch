# 🧠 Machine Learning Project Documentation  
**Day 02: Component & Pipeline Architecture Setup**

## 📁 Folder Structure Creation

### 1️⃣ Inside `src/`, create two key subfolders:
#### 🔹 `components/`
- `__init__.py` – Initializes the module
- `data_ingestion.py` – Handles data loading
- `data_transformation.py` – Preprocessing logic
- `model_trainer.py` – Model training and evaluation

#### 🔹 `pipeline/`
- `__init__.py` – Initializes the module
- `train_pipeline.py` – Orchestrates training workflow
- `predict_pipeline.py` – Handles prediction logic
- `logger.py` – Centralized logging configuration
- `exception.py` – Custom exception handling
- `utils.py` – Utility functions (e.g., file operations, metrics)

---

## 🪵 `logger.py`: Logging Configuration

This module sets up a timestamped log file inside a `logs/` directory.

```python
import logging
import os
from datetime import datetime

LOG_FILE = f"{datetime.now().strftime('%m_%d_%Y_%H_%M_%S')}.log"
logs_path = os.path.join(os.getcwd(), "logs", LOG_FILE)
os.makedirs(logs_path, exist_ok=True)

LOG_FILE_PATH = os.path.join(logs_path, LOG_FILE)

logging.basicConfig(
    filename=LOG_FILE_PATH,
    format="[ %(asctime)s ] %(lineno)d %(name)s - %(levelname)s - %(message)s",
    level=logging.INFO,
)

# Example usage
# if __name__ == "__main__":
#     logging.info("Logging has started")
```

---

## ❗ `exception.py`: Custom Exception Class

This module defines a reusable exception handler that logs detailed error context.

```python
import sys
from src.logger import logging

def error_message_detail(error, error_detail: sys):
    _, _, exc_tb = error_detail.exc_info()
    file_name = exc_tb.tb_frame.f_code.co_filename
    error_message = "Error occurred in script [{0}] at line [{1}]: {2}".format(
        file_name, exc_tb.tb_lineno, str(error)
    )
    return error_message

class CustomException(Exception):
    def __init__(self, error_message, error_detail: sys):
        super().__init__(error_message)
        self.error_message = error_message_detail(error_message, error_detail)

    def __str__(self):
        return self.error_message

# Example usage
# if __name__ == "__main__":
#     try:
#         a = 1 / 0
#     except Exception as e:
#         logging.info("Divide by zero")
#         raise CustomException(e, sys)
```