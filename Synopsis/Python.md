# Python: сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке Python](#що-таке-python)
-   [Історія та роль Python](#історія-та-роль-python)
-   [Встановлення, середовище, запуск коду](#встановлення-середовище-запуск-коду)
-   [Синтаксис: базовий і сучасний](#синтаксис-базовий-і-сучасний)
-   [Структура проекту, модулі та пакети](#структура-проекту-модулі-та-пакети)
-   [Змінні, типи, типізація (type hints)](#змінні-типи-типізація-type-hints)
-   [Функції, замикання (closure), lambda, декоратори](#функції-замикання-closure-lambda-декоратори)
-   [Класи, ООП, dataclass, ABC, метакласи](#класи-ооп-dataclass-abc-метакласи)
-   [Виключення, обробка помилок](#виключення-обробка-помилок)
-   [Колекції: list, dict, set, tuple, comprehension](#колекції-list-dict-set-tuple-comprehension)
-   [Ітератори, генератори, yield](#ітератори-генератори-yield)
-   [Асинхронність: async, await, event loop, asyncio](#асинхронність-async-await-event-loop-asyncio)
-   [Внутрішні механізми: GIL, memory management, garbage collection, performance traps](#внутрішні-механізми-gil-memory-management-garbage-collection-performance-traps)
-   [Файлова система, streams, pathlib, OS](#файлова-система-streams-pathlib-os)
-   [Робота з API, HTTP, requests, aiohttp, FastAPI](#робота-з-api-http-requests-aiohttp-fastapi)
-   [Візуалізація даних (matplotlib, seaborn, plotly)](#візуалізація-даних-matplotlib-seaborn-plotly)
-   [Тестування: pytest, unittest, coverage](#тестування-pytest-unittest-coverage)
-   [Best practices](#best-practices)
-   [Типові підводні камені, security traps](#типові-підводні-камені-security-traps)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**Python** — універсальна, сучасна, високорівнева мова програмування, яка у 2024 році є стандартом для data science, backend, автоматизації, ML/AI, DevOps, scripting, web-розробки, тестування та розробки інструментів.

---

## Що таке Python

-   **Python** — інтерпретована, динамічно типізована, мультипарадигмальна мова.
-   Головні переваги: читабельність, лаконічність, велика екосистема бібліотек, кросплатформенність.
-   Підтримує ООП, функціональне, процедурне програмування, асинхронність.

---

## Історія та роль Python

-   **1991:** Створений Гвідо ван Россумом.
-   **2008:** Python 3 — сучасний стандарт.
-   **2018-2024:** Python — лідер у data science, ML/AI, web, scripting, automation, education.
-   Використовується Google, NASA, Meta, Dropbox, Spotify, Instagram, Reddit.

---

## Встановлення, середовище, запуск коду

### Встановлення

-   [Офіційний сайт](https://www.python.org/downloads/)
-   Рекомендується використовувати **Python 3.12+**.

### Віртуальне середовище

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

### Запуск коду

```bash
python script.py
```

### REPL та Jupyter

-   Інтерактивний режим: `python`
-   [Jupyter Notebook](https://jupyter.org/) — для data science, візуалізації.

---

## Синтаксис: базовий і сучасний

### Hello, world!

```python
print("Hello, Python!")
```

### Змінні, типи

```python
name: str = "Oleg"
score: int = 42
is_active: bool = True
```

### f-strings (сучасний спосіб форматування)

```python
print(f"User {name}: score = {score}")
```

### Множинне присвоєння

```python
x, y = 5, 7
```

### Умови, цикли

```python
if score > 10:
    print("Good!")
else:
    print("Try again!")

for i in range(5):
    print(i)
```

---

## Структура проекту, модулі та пакети

```
my_python_app/
├─ main.py
├─ app/
│   ├─ __init__.py
│   ├─ models.py
│   ├─ utils.py
│   ├─ api.py
│   └─ views.py
├─ tests/
│   └─ test_main.py
├─ requirements.txt
├─ README.md
├─ .env
└─ .gitignore
```

-   **Модулі:** окремі файли `.py`
-   **Пакети:** директорії з `__init__.py`
-   Імпорт модулів: `from app.utils import foo`

---

## Змінні, типи, типізація (type hints)

### Типи змінних

```python
a: int = 10
b: float = 3.14
c: str = "python"
d: list[int] = [1, 2, 3]
e: dict[str, int] = {"a": 1, "b": 2}
```

### Type hints (PEP 484, PEP 604)

```python
def add(a: int, b: int) -> int:
    return a + b

def get_user(id: int) -> dict[str, str] | None:
    ...
```

### Optional, Union

```python
from typing import Optional, Union

def foo(x: Union[int, str]) -> Optional[str]:
    return str(x) if x else None
```

---

## Функції, замикання (closure), lambda, декоратори

### Оголошення функції

```python
def greet(name: str) -> str:
    return f"Hello, {name}!"
```

### Lambda (анонімна функція)

```python
add = lambda x, y: x + y
```

### Замикання (closure)

```python
def make_multiplier(n: int):
    def inner(x: int) -> int:
        return x * n
    return inner

double = make_multiplier(2)
print(double(5))  # 10
```

### Декоратори

```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"Called {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@log
def foo():
    print("Foo")
```

### Сучасні декоратори з type hints

```python
from typing import Callable, TypeVar

T = TypeVar("T")
def log2(func: Callable[..., T]) -> Callable[..., T]:
    def wrapper(*args, **kwargs) -> T:
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper
```

---

## Класи, ООП, dataclass, ABC, метакласи

### Клас (Class)

```python
class User:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def greet(self) -> str:
        return f"Hi, I'm {self.name}"
```

### Наслідування (Inheritance)

```python
class Admin(User):
    def __init__(self, name: str, age: int, level: int):
        super().__init__(name, age)
        self.level = level
```

### Dataclass (PEP 557)

```python
from dataclasses import dataclass

@dataclass
class Product:
    name: str
    price: float
```

### ABC (Abstract Base Class)

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass
```

### Метаклас

```python
class Meta(type):
    def __new__(cls, name, bases, dct):
        print(f"Creating class {name}")
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=Meta):
    pass
```

---

## Виключення, обробка помилок

### try-except-finally

```python
try:
    x = 1 / 0
except ZeroDivisionError as e:
    print("Помилка:", e)
finally:
    print("Завжди виконується")
```

### Власні винятки

```python
class AppError(Exception):
    pass

raise AppError("Щось пішло не так!")
```

---

## Колекції: list, dict, set, tuple, comprehension

### List

```python
numbers: list[int] = [1, 2, 3]
numbers.append(4)
```

### Dict

```python
users: dict[str, int] = {"Oleg": 30, "Anna": 25}
```

### Set

```python
unique: set[int] = {1, 2, 2, 3}
```

### Tuple

```python
point: tuple[int, int] = (2, 5)
```

### List comprehension

```python
squares = [x*x for x in range(10)]
```

### Dict comprehension

```python
user_map = {u: len(u) for u in ["Oleg", "Anna"]}
```

### Генератори (generator expressions)

```python
gen = (x*x for x in range(5))
for val in gen:
    print(val)
```

---

## Ітератори, генератори, yield

### Ітератор

```python
it = iter([1, 2, 3])
print(next(it))
```

### Генератор

```python
def fib(n: int):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

for val in fib(5):
    print(val)
```

### yield from

```python
def chain(*iterables):
    for it in iterables:
        yield from it
```

---

## Асинхронність: async, await, event loop, asyncio

### Асинхронна функція

```python
import asyncio

async def fetch_data():
    await asyncio.sleep(1)
    return "data"

async def main():
    result = await fetch_data()
    print(result)

asyncio.run(main())
```

### Event Loop

-   **asyncio** — стандартний event loop Python.
-   Можна запускати багато задач паралельно.

### Task, gather

```python
async def foo():
    await asyncio.sleep(1)
    return 42

async def main():
    results = await asyncio.gather(foo(), foo())
    print(results)

asyncio.run(main())
```

### aiohttp (HTTP async)

```python
import aiohttp
import asyncio

async def get_page(url: str):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as resp:
            return await resp.text()

asyncio.run(get_page("https://example.com"))
```

---

## Внутрішні механізми: GIL, memory management, garbage collection, performance traps

### GIL (Global Interpreter Lock)

-   GIL — у CPython тільки один потік виконує Python-байткод одночасно.
-   Паралельність — через multiprocessing, asyncio, не через threading.

### Memory management

-   Python автоматично керує пам’яттю (reference counting, garbage collection).
-   `gc` — модуль для контролю GC.

### Garbage Collection

```python
import gc
gc.collect()
```

-   GC типово не вичищає циклічні посилання відразу.

### Performance traps

-   **Великі списки/словники:** оптимізуй структуру.
-   **Невідпущені ресурси:** закривай файли, сокети, потоки (with statement).
-   **Зайва робота з глобальними змінними:** уникай side effects.

### Deep dive-матеріали

-   [Python Memory Management](https://realpython.com/python-memory-management/)
-   [GIL Explained](https://realpython.com/python-gil/)
-   [Asyncio Docs](https://docs.python.org/3/library/asyncio.html)

---

## Файлова система, streams, pathlib, OS

### pathlib

```python
from pathlib import Path
p = Path("myfile.txt")
if p.exists():
    print(p.read_text())
```

### Робота з файлами

```python
with open("data.txt", "w") as f:
    f.write("Hello, World!")
```

### Створення директорії

```python
import os
os.makedirs("data/backup", exist_ok=True)
```

### Streams

-   Читання/запис у великий файл через stream — не завантажуй весь файл у пам’ять.

```python
with open("bigdata.bin", "rb") as f:
    while chunk := f.read(1024):
        process(chunk)
```

---

## Робота з API, HTTP, requests, aiohttp, FastAPI

### requests (sync)

```python
import requests
resp = requests.get("https://api.github.com")
print(resp.json())
```

### aiohttp (async)

```python
import aiohttp
async with aiohttp.ClientSession() as session:
    async with session.get("https://api.github.com") as resp:
        print(await resp.json())
```

### FastAPI (сучасний web-фреймворк)

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    return {"message": "Hello FastAPI"}

# Запуск: uvicorn main:app --reload
```

### Pydantic для валідації

```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name: str
```

---

## Візуалізація даних (matplotlib, seaborn, plotly)

### matplotlib

```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3], [1, 4, 9])
plt.xlabel("x")
plt.ylabel("y")
plt.show()
```

### seaborn

```python
import seaborn as sns
import pandas as pd

df = pd.DataFrame({"x": [1,2,3], "y": [1,4,9]})
sns.lineplot(data=df, x="x", y="y")
```

### plotly (інтерактивна візуалізація)

```python
import plotly.express as px
df = pd.DataFrame({"x": [1,2,3], "y": [1,4,9]})
fig = px.line(df, x="x", y="y", title="My Plot")
fig.show()
```

---

## Тестування: pytest, unittest, coverage

### pytest

```python
def sum(a: int, b: int) -> int:
    return a + b

def test_sum():
    assert sum(2, 3) == 5
```

### unittest

```python
import unittest

class TestMath(unittest.TestCase):
    def test_sum(self):
        self.assertEqual(sum(2, 3), 5)
```

### coverage

```bash
pytest --cov=app
```

---

## Best practices

-   Використовуй віртуальні середовища (`venv`, `poetry`).
-   Дотримуйся PEP8 (стиль коду).
-   Використовуй type hints, dataclass, сучасний синтаксис.
-   Не використовуй глобальні змінні.
-   Діли код на модулі, пакети.
-   Валідуй дані (pydantic, marshmallow).
-   Логуй через стандартний модуль `logging`.
-   Відпускай ресурси через with statement.
-   Пиши юніт- та інтеграційні тести.
-   Документуй код (docstrings, README.md).
-   Оновлюй залежності, перевіряй через `pip-audit`.
-   Використовуй асинхронність для I/O bound задач.
-   Використовуй сучасні фреймворки (FastAPI, aiohttp) для web/API.
-   Очищуй пам’ять і ресурси, профілюй продуктивність.

---

## Типові підводні камені, security traps

-   **GIL:** не дає справжньої багатопоточності у CPython (для CPU-bound задач використовуй multiprocessing).
-   **Mutable default arguments:** не використовуй змінні типу list, dict як default аргументи функції.
-   **Unclosed resources:** завжди закривай файли, сокети (with statement).
-   **Injection:** валідуй всі дані, не передавай дані напряму у exec, eval.
-   **Outdated packages:** регулярно оновлюй залежності.
-   **Circular imports:** розбивай модулі правильно, уникай циклічного імпорту.
-   **Side effects:** уникай логіки у глобальній області видимості.
-   **Відсутність типізації:** використовуй type hints для складних проектів.

---

## Корисні ресурси та документація

-   [Офіційна документація Python](https://docs.python.org/3/)
-   [PEP8 — стиль коду](https://peps.python.org/pep-0008/)
-   [FastAPI Docs](https://fastapi.tiangolo.com/)
-   [Asyncio Docs](https://docs.python.org/3/library/asyncio.html)
-   [Pytest Docs](https://docs.pytest.org/)
-   [Pydantic Docs](https://docs.pydantic.dev/)
-   [Matplotlib Docs](https://matplotlib.org/stable/contents.html)
-   [Seaborn Docs](https://seaborn.pydata.org/)
-   [Plotly Docs](https://plotly.com/python/)
-   [Python Deep Dive Blog](https://realpython.com/)
-   [pip-audit](https://pypi.org/project/pip-audit/)
-   [Python Packaging](https://packaging.python.org/en/latest/)
-   [Python Security Checklist](https://github.com/toniblyx/python-security-guide)

---

## Короткий підсумок

**Python — це сучасна, продуктивна, універсальна мова для бекенду, data science, ML/AI, автоматизації, web, тестування та scripting.**  
Використовуй type hints, dataclass, асинхронність, сучасні фреймворки.  
Дотримуйся best practices, тестуй, профілюй, розбирайся у підкапотних механізмах — і твій Python-код буде відповідати вимогам 2024+!

---
