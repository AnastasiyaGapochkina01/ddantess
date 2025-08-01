# Часть 1
Создать репозиторий в gitlab, подключить к нему runner. В репозитории создать файлы
- `calculator.py` с содержимым
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```
- `test_calculator.py` с содержимым
```python
from calculator import add, subtract

def test_add():
    assert add(3, 5) == 8
    assert add(-1, 1) == 0

def test_subtract():
    assert subtract(10, 4) == 6
    assert subtract(0, 5) == -5
```
Написать pipeline, который при пуше в репозиторий автоматически
- запускает линтер (можно использовать flake8)
- запускает тесты (`pytest test_calculator.py -v`)

# Часть 2
Написать pipeline для приложения https://github.com/AnastasiyaGapochkina01/simple-py/tree/main, который при пуше в репозиторий
- запускает линтер (можно использовать flake8)
- запускает тесты
- собирает docker image (Dockerfile написать самостоятельно)
- пушит image в container registry
- деплоит собранный image на ВМ
- выполняет проверку (`curl -I VM_IP:5000`)
