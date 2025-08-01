# Python Cheatsheet

## Basics
print('Hello, World!')  
x = 5  
y = 3.14  
name = "Ooodysseus"  
is_active = True  
None  
type(x)  
id(x)  
del x  

## Data Types
int, float, str, bool, list, tuple, dict, set, NoneType  

## Variables
x, y, total, name  
x, y = 1, 2  
a, b, c = [1, 2, 3]  
_x, __private, var1  

## Strings
s = 'hello'  
s = "world"  
s = """multiline"""  
s[0]  
len(s)  
s.upper()  
s.lower()  
s.title()  
s.strip()  
s.replace('h', 'j')  
s.split(',')  
','.join(['a','b'])  
f'Hello {name}'  
'abc' in s  

## Numbers
abs(-5)  
round(2.63)  
pow(2, 3)  
max(1, 2, 3)  
min(1, 2, 3)  
sum([1,2,3])  

## Lists
lst = [1,2,3]  
lst.append(4)  
lst.extend([5,6])  
lst.insert(0, 0)  
lst.pop()  
lst.remove(2)  
lst.sort()  
lst.reverse()  
lst.count(3)  
lst.index(1)  
lst.clear()  
len(lst)  
lst[0:2]  
lst[-1]  
[ x*2 for x in lst ]  

## Tuples
t = (1,2,3)  
t[0]  
len(t)  
tuple(lst)  

## Sets
s = {1,2,3}  
s.add(4)  
s.remove(2)  
s.discard(5)  
s.union({5,6})  
s.intersection({2,3})  
s.difference({1})  
len(s)  

## Dicts
d = {'a': 1, 'b': 2}  
d['c'] = 3  
d.get('d', 0)  
d.keys()  
d.values()  
d.items()  
d.pop('a')  
d.update({'e':4})  
del d['b']  
len(d)  
{ k:v for k,v in d.items() }  

## Control Flow
if x > 0:  
    print('Positive')  
elif x == 0:  
    print('Zero')  
else:  
    print('Negative')  

for i in range(5):  
    print(i)  

for key in d:  
    print(key, d[key])  

while x < 10:  
    x += 1  

break  
continue  
pass  

## Functions
def add(a, b):  
    return a + b  

def foo(x=1, y=2):  
    return x + y  

def bar(*args, **kwargs):  
    print(args, kwargs)  

lambda x: x*2  

## Classes
class Animal:  
    def __init__(self, name):  
        self.name = name  
    def speak(self):  
        print(self.name)  

class Dog(Animal):  
    def bark(self):  
        print('Woof!')  

d = Dog('Rex')  
d.speak()  
d.bark()  

## Properties & Methods
@property  
def value(self):  
    return self._value  

@staticmethod  
def foo():  
    pass  

@classmethod  
def bar(cls):  
    pass  

## Exceptions
try:  
    1/0  
except ZeroDivisionError:  
    print('Error')  
except Exception as e:  
    print(e)  
else:  
    print('No error')  
finally:  
    print('Always')  
raise ValueError('fail')  

## Modules & Imports
import math  
import sys  
import os  
from datetime import datetime  
from math import pi, sqrt  
import numpy as np  
from mymodule import foo, bar  

## File I/O
with open('file.txt', 'r') as f:  
    data = f.read()  

with open('file.txt', 'w') as f:  
    f.write('Hello')  

with open('file.txt') as f:  
    for line in f:  
        print(line.strip())  

## OS Operations
os.getcwd()  
os.listdir('.')  
os.remove('file.txt')  
os.rename('a.txt', 'b.txt')  
os.path.exists('file.txt')  
os.path.join('dir','file.txt')  

## Sys Operations
sys.argv  
sys.exit(0)  
sys.path  
sys.version  

## Date & Time
from datetime import datetime, timedelta  
now = datetime.now()  
today = datetime.today()  
dt = datetime.strptime('2025-08-01', '%Y-%m-%d')  
dt.strftime('%d/%m/%Y')  
timedelta(days=5)  

## Math
math.sqrt(9)  
math.ceil(2.1)  
math.floor(2.9)  
math.pi  
round(1.23, 1)  

## Random
import random  
random.randint(1,10)  
random.choice(['a','b','c'])  
random.shuffle(lst)  
random.sample(lst, 2)  

## JSON
import json  
json.dumps({'a':1})  
json.loads('{"a":1}')  

## Regular Expressions
import re  
re.match(r'\d+', '123')  
re.search(r'ab', 'abc')  
re.findall(r'\w+', 'a b c')  
re.sub(r'\s+', '-', 'a b c')  

## Virtual Environment
python -m venv venv  
source venv/bin/activate  
pip install package  
pip freeze > requirements.txt  
pip install -r requirements.txt  

## Pip
pip install package  
pip uninstall package  
pip list  
pip freeze  

## Arguments
import argparse  
parser = argparse.ArgumentParser()  
parser.add_argument('--val')  
args = parser.parse_args()  
print(args.val)  

## Decorators
def dec(fn):  
    def wrapper(*a, **k):  
        print('Before'); return fn(*a, **k)  
    return wrapper  

@dec  
def foo():  
    pass  

## Type Hints
def add(a: int, b: int) -> int:  
    return a + b  

## Docstrings
def foo():  
    """This does foo."""  
    pass  

## List Comprehensions
[x*2 for x in range(5)]  
[x for x in lst if x > 1]  

## Generators
def gen():  
    yield 1  
    yield 2  
for x in gen():  
    print(x)  

## Context Managers
with open('file.txt') as f:  
    data = f.read()  

## Enumerate & Zip
for i, v in enumerate(lst):  
    print(i, v)  
for a, b in zip(lst1, lst2):  
    print(a, b)  

## Map, Filter, Reduce
list(map(str, lst))  
list(filter(lambda x: x>1, lst))  
from functools import reduce  
reduce(lambda a,b: a+b, lst)  

## Collections
from collections import Counter, defaultdict, namedtuple  
Counter(lst)  
d = defaultdict(int)  
Point = namedtuple('Point', 'x y')  
p = Point(1,2)  

## Dataclasses
from dataclasses import dataclass  
@dataclass  
class User:  
    name: str  
    age: int  

## Set Operations
set([1,2,3]) | set([2,3,4])  
set([1,2,3]) & set([2,3,4])  
set([1,2,3]) - set([2])  

## Sorting
sorted(lst)  
lst.sort(reverse=True)  
sorted(d.items(), key=lambda x: x[1])  

## Lambda
lambda x: x + 1  

## Unpacking
a, b, *rest = [1,2,3,4]  

## Slicing
lst[1:3]  
lst[::-1]  

## Main Guard
if __name__ == '__main__':  
    main()  

## Unit Testing
import unittest  
class TestFoo(unittest.TestCase):  
    def test_add(self):  
        self.assertEqual(add(1,2), 3)  
unittest.main()  

## Logging
import logging  
logging.basicConfig(level=logging.INFO)  
logging.info('Message')  

## HTTP Requests
import requests  
r = requests.get('https://api.com')  
r.json()  
r.status_code  

## Flask Example
from flask import Flask  
app = Flask(__name__)  
@app.route('/')  
def home():  
    return 'Hello'  
if __name__ == '__main__':  
    app.run()  

## Async
import asyncio  
async def foo():  
    await asyncio.sleep(1)  
asyncio.run(foo())  

## Type Checking
isinstance(x, int)  
issubclass(Dog, Animal)  

## Best Practices
Use virtualenv  
Write docstrings  
Comment complex logic  
Use type hints  
Limit global variables  
Organize code in modules  
Test with unittest/pytest  
Handle exceptions  
Validate user input  
Avoid hardcoded values  
Use requirements.txt  
Keep functions small  
Minimize side effects  
Use context managers  
Use list comprehensions  
Keep code readable  
Follow PEP 8  
Refactor old code  
Version scripts  
Document APIs  
Automate deployment  
Use logging  
Monitor performance  
Limit third-party packages  
Backup regularly  
Review dependencies  
Use pip freeze  
Optimize algorithms  
Use proper naming  
Keep changelog  
Test edge cases  
Use decorators  
Prefer simple solutions  
Limit magic numbers  
Support multiple platforms  
Minimize external dependencies  
Handle missing files  
Automate testing  
Keep main guard  
Comment intent  
Archive unused code  
Optimize imports  
Test user flows  
Monitor error logs  
Validate config  
Review updates  
Keep README updated  
Automate builds  
Support containers  
Keep structure logical  
Optimize for scale  
