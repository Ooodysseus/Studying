# PYTHON

Python — універсальна мова програмування для скриптів, вебу, науки, автоматизації, ML, з величезною екосистемою бібліотек.

## Категорія: Основи синтаксису

| Команда/метод            | Опис                 | Приклад/Аутпут                    |
| ------------------------ | -------------------- | --------------------------------- |
| print()                  | вивід                | print('Hello') → Hello            |
| input()                  | введення             | input('Name: ')                   |
| #, '''...'''             | коментарі            | # однорядковий, '''багаторядк.''' |
| if/elif/else             | умовні оператори     | if x>0: ... elif x==0: ...        |
| for/while/break/continue | цикли                | for i in range(3): ...            |
| def func():              | функція              | def f(x): return x+1              |
| return                   | повернути значення   | return x                          |
| pass                     | пуста інструкція     | if x: pass                        |
| None                     | відсутність значення | x = None                          |
| True/False               | булеві значення      | x = True                          |
| and/or/not               | логічні оператори    | if a and not b: ...               |
| in/not in                | перевірка належності | if x in arr: ...                  |

## Категорія: Робота з числами, рядками

| Команда/метод         | Опис                | Приклад/Аутпут                 |
| --------------------- | ------------------- | ------------------------------ |
| int(), float(), str() | приведення типу     | int('5') → 5                   |
| len()                 | довжина             | len('abc') → 3                 |
| 'a' + 'b', 'a'\*3     | конкатенація/повтор | 'a'+'b' → 'ab', 'a'\*3 → 'aaa' |
| s.upper(), s.lower()  | регістр             | 'abc'.upper() → 'ABC'          |
| s.split(), s.join()   | розбити/з'єднати    | 'a,b'.split(',') → ['a','b']   |
| s.replace('a','b')    | заміна              | 'aab'.replace('a','b') → 'bbb' |
| s.strip()             | обрізка пробілів    | ' a '.strip() → 'a'            |
| s.find('x')           | пошук               | 'abc'.find('b') → 1            |

## Категорія: Списки, кортежі, множини, словники

| Команда/метод        | Опис               | Приклад/Аутпут              |
| -------------------- | ------------------ | --------------------------- |
| [1,2,3], list()      | список             | list('abc') → ['a','b','c'] |
| .append(), .extend() | додати елементи    | arr.append(4)               |
| .pop(), .remove()    | видалити елемент   | arr.pop() → 3               |
| .sort(), sorted()    | сортування         | arr.sort(), sorted(arr)     |
| (1,2,3), tuple()     | кортеж             | tuple([1,2]) → (1,2)        |
| {1,2,3}, set()       | множина            | set([1,2,2]) → {1,2}        |
| .add(), .discard()   | додати/видалити    | s.add(4), s.discard(2)      |
| {'a':1}, dict()      | словник            | dict(a=1) → {'a':1}         |
| .keys(), .values()   | ключі/значення     | d.keys(), d.values()        |
| .items()             | пари ключ-значення | d.items()                   |
| .get('a',0)          | отримати значення  | d.get('a',0)                |

## Категорія: Функції, lambda, map/filter/reduce

| Команда/метод                | Опис                | Приклад/Аутпут                    |
| ---------------------------- | ------------------- | --------------------------------- |
| def f(x): ...                | функція             | def f(x): return x+1              |
| lambda x: x+1                | анонімна функція    | lambda x: x\*2                    |
| map(f, arr)                  | застосувати функцію | list(map(str, [1,2])) → ['1','2'] |
| filter(f, arr)               | фільтрація          | list(filter(lambda x:x>0, arr))   |
| from functools import reduce | reduce              | reduce(lambda a,b:a+b, arr)       |
| \*args, \*\*kwargs           | довільні аргументи  | def f(\*a,\*\*k): ...             |
| return                       | повернути значення  | return x                          |

## Категорія: Класи, ООП

| Команда/метод       | Опис                  | Приклад/Аутпут                  |
| ------------------- | --------------------- | ------------------------------- |
| class X: ...        | клас                  | class X: pass                   |
| def **init**(self): | конструктор           | def **init**(self, x): self.x=x |
| self                | поточний екземпляр    | self.x = 5                      |
| @staticmethod       | статичний метод       | @staticmethod def f(): ...      |
| @classmethod        | класовий метод        | @classmethod def f(cls): ...    |
| super()             | батьківський клас     | super().**init**()              |
| **str**, **repr**   | рядкове представлення | def **str**(self): ...          |
| Наслідування        | class B(A): ...       | class B(A): ...                 |

## Категорія: Модулі, імпорт, робота з файлами

| Команда/метод             | Опис             | Приклад/Аутпут                       |
| ------------------------- | ---------------- | ------------------------------------ |
| import x, from x import y | імпорт           | import math, from os import path     |
| as                        | псевдонім        | import numpy as np                   |
| open('f') as f            | відкрити файл    | with open('f') as f: ...             |
| f.read(), f.write()       | читати/писати    | f.read(), f.write('hi')              |
| os.listdir(), os.path     | робота з файлами | os.listdir('.'), os.path.exists('f') |

## Категорія: Винятки, assert, типізація

| Команда/метод          | Опис            | Приклад/Аутпут                |
| ---------------------- | --------------- | ----------------------------- |
| try/except/finally     | обробка помилок | try: ... except: ...          |
| raise                  | кинути виняток  | raise ValueError('err')       |
| assert                 | перевірка       | assert x > 0                  |
| type hints             | підказки типів  | def f(x: int) -> str: ...     |
| from typing import ... | типізація       | from typing import List, Dict |

## Категорія: Стандартні бібліотеки

| Модуль/метод | Опис              | Приклад/Аутпут                       |
| ------------ | ----------------- | ------------------------------------ |
| math, random | математика/рандом | math.sqrt(4), random.randint(1,6)    |
| datetime     | дати/час          | datetime.datetime.now()              |
| json, csv    | робота з даними   | json.loads('{"a":1}'), csv.reader(f) |
| re           | регулярки         | re.match(r'\d+', '123')              |
| sys, os      | системні          | sys.argv, os.environ                 |
| requests     | HTTP-запити       | requests.get('https://...')          |
| subprocess   | shell-команди     | subprocess.run(['ls'])               |

## Категорія: pip, venv, best practices

| Команда/метод       | Опис                    | Приклад/Аутпут                  |
| ------------------- | ----------------------- | ------------------------------- |
| pip install x       | встановити пакет        | pip install requests            |
| python -m venv venv | створити вірт. оточення | python -m venv venv             |
| .venv/bin/activate  | активувати venv         | source venv/bin/activate        |
| requirements.txt    | список залежностей      | pip install -r requirements.txt |
| **main**            | точка входу             | if **name** == '**main**': ...  |
| PEP8                | стиль коду              | flake8, black                   |
| Документація        | help(), docstring       | help(str), def f(): """doc"""   |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
