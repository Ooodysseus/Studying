# Розширена шпаргалка по JavaScript

## ЗМІСТ

1. [Основи синтаксису](#основи-синтаксису)
2. [Типи даних](#типи-даних)
3. [Оператори](#оператори)
4. [Функції](#функції)
5. [Управління потоком](#управління-потоком)
6. [Цикли](#цикли)
7. [Масиви](#масиви)
8. [Об'єкти](#обєкти)
9. [Класи та ООП](#класи-та-ооп)
10. [Модулі](#модулі)
11. [Робота з DOM](#робота-з-dom)
12. [Події](#події)
13. [Асинхронність (Promise, async/await)](#асинхронність-promise-asyncawait)
14. [Робота з JSON](#робота-з-json)
15. [Робота з LocalStorage](#робота-з-localstorage)
16. [Регулярні вирази](#регулярні-вирази)
17. [Корисні методи String та Number](#корисні-методи-string-та-number)
18. [Деструктуризація](#деструктуризація)
19. [Spread/Rest оператори](#spreadrest-оператори)
20. [Set, Map](#set-map)
21. [Error Handling](#error-handling)
22. [Корисні поради](#корисні-поради)

---

## Основи синтаксису

```js
// Коментар
let x = 5; // змінна
const y = 10; // константа
var z = 15; // старий спосіб

// шаблонні рядки
let name = "Іван";
console.log(`Привіт, ${name}!`);
```

---

## Типи даних

-   Number: 10, 3.14, NaN, Infinity
-   String: "hello", 'world', `string`
-   Boolean: true, false
-   Null: null
-   Undefined: undefined
-   Object: { a: 1 }
-   Array: [1, 2, 3]
-   Symbol: Symbol("id")
-   BigInt: 12345678901234567890n

```js
typeof 42; // "number"
typeof "hello"; // "string"
typeof true; // "boolean"
typeof undefined; // "undefined"
typeof null; // "object"
```

---

## Оператори

-   Арифметичні: +, -, \*, /, %, \*\*
-   Порівняння: ==, ===, !=, !==, >, <, >=, <=
-   Логічні: &&, ||, !
-   Присвоєння: =, +=, -=, \*=, /=, %=
-   Тернарний: `умова ? значення1 : значення2`
-   Інкремент/декремент: x++, x--

---

## Функції

```js
function greet(name) {
    return `Привіт, ${name}!`;
}

const sum = (a, b) => a + b; // стрілочна функція

// Значення за замовчуванням
function pow(x = 2, y = 3) {
    return x ** y;
}

// Анонімна функція
setTimeout(function () {
    console.log("Hi");
}, 1000);
```

---

## Управління потоком

```js
if (x > 10) {
    // ...
} else if (x > 5) {
    // ...
} else {
    // ...
}

switch (color) {
    case "red":
        break;
    case "blue":
        break;
    default:
        break;
}
```

---

## Цикли

```js
for (let i = 0; i < 10; i++) {
    /* ... */
}

while (cond) {
    /* ... */
}

do {
    /* ... */
} while (cond);

for (const item of arr) {
    /* ... */
}
for (const key in obj) {
    /* ... */
}

arr.forEach((val, idx) => {
    /* ... */
});
arr.map((x) => x * 2);
arr.filter((x) => x > 2);
```

---

## Масиви

```js
let arr = [1, 2, 3];
arr.length; // довжина
arr.push(4); // додати в кінець
arr.pop(); // видалити з кінця
arr.shift(); // видалити з початку
arr.unshift(0); // додати на початок

arr.slice(1, 3); // новий масив
arr.splice(2, 1, 10); // змінює масив
arr.indexOf(2); // індекс
arr.includes(3); // true/false

arr.reverse(); // перевертає
arr.sort((a, b) => a - b); // сортує

[...arr]; // копія
```

---

## Об'єкти

```js
let user = { name: "Anna", age: 25 };
user.name;
user["age"];

user.city = "Kyiv";
delete user.age;

Object.keys(user); // ["name", "city"]
Object.values(user); // ["Anna", "Kyiv"]
Object.entries(user); // [["name", "Anna"], ["city", "Kyiv"]]

let clone = { ...user }; // копія
```

---

## Класи та ООП

```js
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} говорить`);
    }
}

class Dog extends Animal {
    speak() {
        super.speak();
        console.log("Гав!");
    }
}

let d = new Dog("Барон");
d.speak();
```

---

## Модулі

```js
// file.js
export const x = 10;
export default function hello() {}

// main.js
import { x } from "./file.js";
import hello from "./file.js";
```

---

## Робота з DOM

```js
document.getElementById("id");
document.querySelector(".class");
document.querySelectorAll("div");

element.textContent = "Текст";
element.innerHTML = "<b>HTML</b>";
element.value = "input value";

element.style.background = "yellow";
element.classList.add("active");
element.classList.remove("active");

element.setAttribute("data-x", "123");
element.getAttribute("data-x");
element.removeAttribute("data-x");
```

---

## Події

```js
element.addEventListener("click", function (e) {
    console.log("Клік");
});

function handler(e) {
    e.preventDefault();
    e.stopPropagation();
}

element.removeEventListener("click", handler);
```

---

## Асинхронність (Promise, async/await)

### setTimeout / setInterval

```js
setTimeout(() => {
    /* ... */
}, 1000);
setInterval(() => {
    /* ... */
}, 1000);
clearTimeout(timer);
clearInterval(interval);
```

### Promise

```js
let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("OK"), 1000);
});

promise.then((res) => console.log(res)).catch((err) => console.error(err));
```

### async/await

```js
async function getData() {
    try {
        let res = await fetch(url);
        let data = await res.json();
        return data;
    } catch (err) {
        console.error(err);
    }
}
```

---

## Робота з JSON

```js
let obj = { a: 1, b: 2 };
let json = JSON.stringify(obj);
let obj2 = JSON.parse(json);
```

---

## Робота з LocalStorage

```js
localStorage.setItem("key", "value");
localStorage.getItem("key");
localStorage.removeItem("key");
localStorage.clear();
```

---

## Регулярні вирази

```js
let str = "hello123";
let re = /\d+/;
re.test(str); // true
str.match(re); // ["123"]
str.replace(/\d+/, "!");
```

---

## Корисні методи String та Number

```js
let str = "  Hello, JS!  ";
str.length;
str.toUpperCase();
str.toLowerCase();
str.trim();
str.startsWith("Hello");
str.endsWith("JS!");
str.includes("JS");
str.replace("JS", "World");
str.split(",");
str.repeat(2);

let n = 5.67;
Math.round(n); // 6
Math.floor(n); // 5
Math.ceil(n); // 6
Math.abs(-42); // 42
Math.max(1, 2, 3); // 3
Math.min(1, 2, 3); // 1
Math.random(); // 0..1
parseInt("42px"); // 42
parseFloat("3.14m"); // 3.14
```

---

## Деструктуризація

```js
let arr = [1, 2, 3];
let [a, b, c] = arr;

let obj = { name: "Anna", age: 22 };
let { name, age } = obj;

// Вкладена деструктуризація
let {
    address: { city },
} = { address: { city: "Lviv" } };
```

---

## Spread/Rest оператори

```js
let arr = [1, 2, 3];
let arr2 = [...arr, 4, 5];

function sum(...nums) {
    return nums.reduce((a, b) => a + b);
}

let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 };
```

---

## Set, Map

```js
let set = new Set([1, 2, 2, 3]);
set.add(4);
set.has(2);
set.delete(1);

let map = new Map();
map.set("a", 1);
map.get("a");
map.delete("a");
for (let [key, val] of map) {
    /* ... */
}
```

---

## Error Handling

```js
try {
    throw new Error("Помилка!");
} catch (e) {
    console.error(e.message);
} finally {
    console.log("Завжди виконується");
}
```

---

## Корисні поради

-   Копія масиву: `[...arr]`
-   Копія об'єкта: `{...obj}`
-   Перевірка на undefined: `if (typeof x !== "undefined")`
-   Перевірка на NaN: `isNaN(value)`
-   Перевірка масиву: `Array.isArray(arr)`
-   Перевірка об'єкта: `typeof obj === "object" && !Array.isArray(obj)`
-   Перевірка числа: `typeof n === "number" && !isNaN(n)`

---

## Корисні ресурси

-   [MDN Web Docs](https://developer.mozilla.org/uk/docs/Web/JavaScript)
-   [JavaScript.info](https://uk.javascript.info/)
-   [w3schools JS](https://www.w3schools.com/js/)
