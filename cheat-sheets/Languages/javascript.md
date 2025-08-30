# JAVASCRIPT

JavaScript — мова для створення інтерактивних веб-сторінок.

## Категорія: Робота з масивами

| Команда/метод            | Опис               | Приклад/Аутпут                      |
| ------------------------ | ------------------ | ----------------------------------- |
| arr.push(4)              | додати елемент     | [1,2,3].push(4) → [1,2,3,4]         |
| arr.pop()                | видалити останній  | [1,2,3].pop() → 3                   |
| arr.shift()              | видалити перший    | [1,2,3].shift() → 1                 |
| arr.unshift(0)           | додати на початок  | [1,2,3].unshift(0) → [0,1,2,3]      |
| arr.includes(2)          | чи є елемент       | [1,2,3].includes(2) → true          |
| arr.indexOf(2)           | індекс елемента    | [1,2,3].indexOf(2) → 1              |
| arr.find(x=>x>1)         | знайти елемент     | [1,2,3].find(x=>x>1) → 2            |
| arr.findIndex(x=>x>1)    | індекс за умовою   | [1,2,3].findIndex(x=>x>1) → 1       |
| arr.map(x=>x\*2)         | новий масив        | [1,2,3].map(x=>x\*2) → [2,4,6]      |
| arr.filter(x=>x>1)       | фільтрація         | [1,2,3].filter(x=>x>1) → [2,3]      |
| arr.reduce((a,b)=>a+b,0) | акумуляція         | [1,2,3].reduce((a,b)=>a+b,0) → 6    |
| arr.slice(1,3)           | зріз               | [1,2,3,4].slice(1,3) → [2,3]        |
| arr.splice(1,2)          | видалити/замінити  | [1,2,3,4].splice(1,2) → [2,3]       |
| arr.concat([4,5])        | об'єднання масивів | [1,2,3].concat([4,5]) → [1,2,3,4,5] |
| arr.join('-')            | рядок з масиву     | [1,2,3].join('-') → '1-2-3'         |
| arr.reverse()            | змінити порядок    | [1,2,3].reverse() → [3,2,1]         |
| arr.sort()               | сортування         | [3,1,2].sort() → [1,2,3]            |
| arr.every(x=>x>0)        | всі відповідають   | [1,2,3].every(x=>x>0) → true        |
| arr.some(x=>x>2)         | хоча б один        | [1,2,3].some(x=>x>2) → true         |
| Array.isArray(arr)       | перевірка масиву   | Array.isArray([1,2,3]) → true       |

## Категорія: Робота з об'єктами

| Команда/метод           | Опис                  | Приклад/Аутпут                     |
| ----------------------- | --------------------- | ---------------------------------- |
| obj.hasOwnProperty('a') | чи є властивість      | {a:1}.hasOwnProperty('a') → true   |
| Object.keys(obj)        | ключі об'єкта         | Object.keys({a:1,b:2}) → ['a','b'] |
| Object.values(obj)      | значення об'єкта      | Object.values({a:1,b:2}) → [1,2]   |
| Object.entries(obj)     | пари ключ-значення    | Object.entries({a:1}) → [['a',1]]  |
| Object.assign({}, obj)  | копіювання/злиття     | Object.assign({}, {a:1}) → {a:1}   |
| obj.a                   | доступ до властивості | ({a:1}).a → 1                      |
| delete obj.a            | видалити властивість  | let o={a:1}; delete o.a; o → {}    |
| 'a' in obj              | чи є ключ             | 'a' in {a:1} → true                |
| Object.freeze(obj)      | заморозити об'єкт     | Object.freeze({a:1})               |
| Object.seal(obj)        | запечатати об'єкт     | Object.seal({a:1})                 |
| Object.hasOwn(obj,'a')  | чи є власний ключ     | Object.hasOwn({a:1},'a') → true    |

## Категорія: Робота з рядками

| Команда/метод        | Опис                | Приклад/Аутпут                     |
| -------------------- | ------------------- | ---------------------------------- |
| str.toUpperCase()    | до великих літер    | 'abc'.toUpperCase() → 'ABC'        |
| str.toLowerCase()    | до малих літер      | 'ABC'.toLowerCase() → 'abc'        |
| str.includes('a')    | чи містить підрядок | 'abc'.includes('a') → true         |
| str.startsWith('a')  | починається з       | 'abc'.startsWith('a') → true       |
| str.endsWith('c')    | закінчується на     | 'abc'.endsWith('c') → true         |
| str.indexOf('b')     | індекс символу      | 'abc'.indexOf('b') → 1             |
| str.slice(1,2)       | підрядок            | 'abc'.slice(1,2) → 'b'             |
| str.substring(1,3)   | підрядок            | 'abc'.substring(1,3) → 'bc'        |
| str.replace('a','x') | заміна              | 'abc'.replace('a','x') → 'xbc'     |
| str.split(',')       | розбити на масив    | 'a,b,c'.split(',') → ['a','b','c'] |
| str.trim()           | обрізати пробіли    | ' abc '.trim() → 'abc'             |
| str.repeat(2)        | повторити           | 'ab'.repeat(2) → 'abab'            |
| str.padStart(5,'0')  | доповнити зліва     | '42'.padStart(5,'0') → '00042'     |
| str.padEnd(5,'0')    | доповнити справа    | '42'.padEnd(5,'0') → '42000'       |

## Категорія: Робота з числами

| Команда/метод      | Опис            | Приклад/Аутпут            |
| ------------------ | --------------- | ------------------------- |
| Math.round(1.6)    | округлення      | Math.round(1.6) → 2       |
| Math.floor(1.6)    | вниз до цілого  | Math.floor(1.6) → 1       |
| Math.ceil(1.2)     | вгору до цілого | Math.ceil(1.2) → 2        |
| Math.max(1,2,3)    | максимум        | Math.max(1,2,3) → 3       |
| Math.min(1,2,3)    | мінімум         | Math.min(1,2,3) → 1       |
| Math.abs(-5)       | модуль числа    | Math.abs(-5) → 5          |
| Math.random()      | випадкове число | Math.random() → 0.123...  |
| Number('42')       | до числа        | Number('42') → 42         |
| parseInt('42px')   | ціле з рядка    | parseInt('42px') → 42     |
| parseFloat('3.14') | дробове з рядка | parseFloat('3.14') → 3.14 |
| (42).toString()    | до рядка        | (42).toString() → '42'    |

## Категорія: Асинхронність

| Команда/метод         | Опис                | Приклад/Аутпут                                               |
| --------------------- | ------------------- | ------------------------------------------------------------ |
| setTimeout(fn, 1000)  | відкласти виконання | setTimeout(()=>console.log('hi'),1000)                       |
| setInterval(fn, 500)  | інтервал виконання  | setInterval(()=>console.log('tick'),500)                     |
| clearTimeout(id)      | скасувати timeout   | clearTimeout(id)                                             |
| clearInterval(id)     | скасувати interval  | clearInterval(id)                                            |
| Promise.resolve(5)    | створити resolved   | Promise.resolve(5).then(x=>x\*2) → 10                        |
| Promise.reject('err') | створити rejected   | Promise.reject('err').catch(e=>e) → 'err'                    |
| Promise.all([p1,p2])  | всі проміси         | Promise.all([Promise.resolve(1),Promise.resolve(2)]) → [1,2] |
| Promise.race([p1,p2]) | перший проміс       | Promise.race([Promise.resolve(1),Promise.resolve(2)]) → 1    |
| async/await           | синтаксис async     | await Promise.resolve(1) → 1                                 |

## Категорія: Модулі

| Команда/метод             | Опис               | Приклад/Аутпут                    |
| ------------------------- | ------------------ | --------------------------------- |
| export default x          | експорт за замовч. | export default function() {}      |
| export const x = 1        | експорт константи  | export const x = 1                |
| export function fn()      | експорт функції    | export function fn() {}           |
| import x from 'mod'       | імпорт за замовч.  | import x from './file.js'         |
| import {x, y} from 'm'    | іменований імпорт  | import {x, y} from './file.js'    |
| import \* as mod from 'm' | імпорт всього      | import \* as mod from './file.js' |
