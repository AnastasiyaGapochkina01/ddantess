## Задача
Создать модульный GitLab CI/CD пайплайн для тестирования Python-приложения, используя:
- разделение логики на шаблоны (include)
- матрицу параллельных тестов (parallel:matrix) для разных версий Python и ОС.

Структура пайплайна:
- этап build: Сборка Docker-образа с приложением.
- этап test:
  - unit-tests: запуск unit-тестов (одна задача).
  - integration-tests: gараллельный запуск интеграционных тестов через матрицу (Python 3.8/3.9 на Ubuntu/Alpine).
 
## Файлы приложения и тестов
- app.py
```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/health')
def health():
    return jsonify({"status": "ok"}), 200

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```
- test_app.py
```python
import pytest
import requests
from app import app

@pytest.fixture
def client():
    app.config['TESTING'] = True
    with app.test_client() as client:
        yield client

# Unit test
def test_health_endpoint(client):
    response = client.get('/health')
    assert response.status_code == 200
    assert response.json == {"status": "ok"}

# Integration test
def test_health_header():
    response = requests.get("http://localhost:5000/health")
    assert response.headers['Content-Type'] == 'application/json'
```
- requirements.txt
```txt
flask
pytest
requests
```
- Dockerfile
```
ARG PYTHON_VERSION=3.9
FROM python:$PYTHON_VERSION-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .
ENTRYPOINT ["python", "app.py"]
```
