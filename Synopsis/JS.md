# JavaScript (JS): сучасний конспект

---

## Зміст

-   [Вступ](#вступ)
-   [Основи JavaScript](#основи-javascript)
-   [Змінні та типи даних](#змінні-та-типи-даних)
-   [Оператори](#оператори)
-   [Умовні конструкції](#умовні-конструкції)
-   [Цикли](#цикли)
-   [Функції](#функції)
-   [Об'єкти та масиви](#об'єкти-та-масиви)
-   [Класи та ООП](#класи-та-ооп)
-   [Модулі та імпорт/експорт](#модулі-та-імпорт-експорт)
-   [Асинхронність: Promise, async/await](#асинхронність-promise-asyncawait)
-   [Робота з DOM](#робота-з-dom)
-   [Події](#події)
-   [Помилки та обробка винятків](#помилки-та-обробка-винятків)
-   [Web APIs: Fetch, LocalStorage, Geolocation](#web-apis-fetch-localstorage-geolocation)
-   [Сучасний синтаксис ES6+](#сучасний-синтаксис-es6)
-   [Фреймворки та бібліотеки](#фреймворки-та-бібліотеки)
-   [Best Practices](#best-practices)
-   [Типові помилки та їх уникнення](#типові-помилки-та-їх-уникнення)
-   [FAQ](#faq)
-   [Корисні ресурси](#корисні-ресурси)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**JavaScript (JS)** — це високорівнева, динамічна мова програмування, яка є стандартом для розробки інтерактивних веб-додатків. З 2024 року JS підтримує сучасний синтаксис (ES6+), розширені можливості роботи з асинхронністю, модульністю, а також має потужну екосистему фреймворків (React, Vue, Next.js, Svelte тощо).

---

## Основи JavaScript

JS виконується у браузері та на сервері (через Node.js).  
Він підтримує об’єктно-орієнтований, функціональний та імперативний стилі програмування.

### Приклад

```js
// Вивід повідомлення у консоль
console.log("Вітаю у світі JavaScript!");
```

---

## Змінні та типи даних

### Оголошення змінних

-   `let` — блочно-обмежена, дозволяє змінювати значення.
-   `const` — блочно-обмежена, не дозволяє змінювати посилання (але можна змінювати властивості об’єкта).
-   `var` — застарілий, не рекомендується до використання.

```js
let age = 25;
const name = "Олександр";
var oldSchool = "Застаріло";
```

### Типи даних

-   **Примітивні:** `string`, `number`, `boolean`, `null`, `undefined`, `bigint`, `symbol`
-   **Складені:** `object`, `array`, `function`

```js
const str = "Текст"; // string
const num = 42; // number
const bool = true; // boolean
const nothing = null; // null
let notDefined; // undefined
const big = 123n; // bigint
const symb = Symbol("id"); // symbol
const obj = { name: "Іван" }; // object
const arr = [1, 2, 3]; // array
const func = () => {}; // function
```

#### Best practice

-   Використовуйте `const` для значень, які не змінюються.
-   Використовуйте `let` у циклах або там, де потрібно змінювати значення.
-   Не використовуйте `var` у сучасних проєктах.

---

## Оператори

### Арифметичні

```js
const sum = 2 + 3; // Додавання
const diff = 5 - 2; // Віднімання
const prod = 3 * 4; // Множення
const div = 10 / 2; // Ділення
const mod = 5 % 2; // Остача
const exp = 2 ** 3; // Степінь
```

### Логічні

```js
const and = true && false; // І
const or = true || false; // АБО
const not = !true; // НЕ
```

### Порівняння

```js
2 == "2"; // true (нестрога рівність)
2 === "2"; // false (строга рівність, враховується тип)
2 != "2"; // false
2 !== "2"; // true
5 > 3; // true
5 <= 3; // false
```

### Тернарний оператор

```js
const status = age >= 18 ? "Дорослий" : "Дитина";
```

### Оператор нульового злиття (nullish coalescing)

```js
const value = userInput ?? "За замовчуванням";
```

---

## Умовні конструкції

### if / else

```js
if (age > 18) {
    console.log("Дорослий");
} else if (age === 18) {
    console.log("Щойно став дорослим");
} else {
    console.log("Дитина");
}
```

### switch

```js
switch (color) {
    case "red":
        console.log("Червоний");
        break;
    case "blue":
        console.log("Синій");
        break;
    default:
        console.log("Інший колір");
}
```

---

## Цикли

### for

```js
for (let i = 0; i < 5; i++) {
    console.log(`Ітерація: ${i}`);
}
```

### while

```js
let i = 0;
while (i < 3) {
    console.log(i);
    i++;
}
```

### do...while

```js
let i = 0;
do {
    console.log(i);
    i++;
} while (i < 3);
```

### for...of (для масивів та ітерованих об'єктів)

```js
const arr = ["a", "b", "c"];
for (const item of arr) {
    console.log(item); // a, b, c
}
```

### for...in (для властивостей об'єкта)

```js
const user = { name: "Іван", age: 22 };
for (const key in user) {
    console.log(key, user[key]);
}
```

---

## Функції

### Оголошення функцій

```js
function greet(name) {
    return `Вітаю, ${name}!`;
}
```

### Анонімні та стрілочні функції

```js
const sum = function (a, b) {
    return a + b;
};
const multiply = (a, b) => a * b; // Стрілочна функція
```

### Параметри за замовчуванням

```js
function showMessage(msg = "Привіт") {
    console.log(msg);
}
```

### Рест-оператор (`...args`)

```js
function total(...nums) {
    return nums.reduce((acc, n) => acc + n, 0);
}
```

### Функції вищого порядку

```js
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((n) => n * 2); // [2, 4, 6, 8]
```

#### Best practice

-   Використовуйте стрілочні функції для коротких колбеків.
-   Додавайте параметри за замовчуванням для гнучкості.
-   Іменуйте функції зрозуміло.

---

## Об'єкти та масиви

### Об'єкти

```js
const user = {
    name: "Марія",
    age: 25,
    isActive: true,
    greet() {
        console.log(`Привіт, я ${this.name}`);
    },
};
user.greet();
```

### Деструктуризація

```js
const { name, age } = user;
console.log(name, age);
```

### Операції над об’єктами

```js
const updatedUser = { ...user, age: 26 }; // Копіювання з оновленням властивості
```

### Масиви

```js
const fruits = ["apple", "banana", "pear"];
console.log(fruits[0]); // apple
```

### Деструктуризація масивів

```js
const [first, second] = fruits;
console.log(first, second); // apple banana
```

### Методи масивів

```js
fruits.push("orange"); // додати елемент
fruits.pop(); // видалити останній
const newFruits = fruits.map((fruit) => fruit.toUpperCase());
const filtered = fruits.filter((fruit) => fruit !== "banana");
```

---

## Класи та ООП

### Оголошення класу

```js
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} говорить`);
    }
}
const dog = new Animal("Барсик");
dog.speak();
```

### Наслідування

```js
class Dog extends Animal {
    speak() {
        console.log(`${this.name} гавкає`);
    }
}
const myDog = new Dog("Рекс");
myDog.speak(); // Рекс гавкає
```

### Статичні методи та властивості

```js
class MathUtils {
    static sum(a, b) {
        return a + b;
    }
}
console.log(MathUtils.sum(2, 3)); // 5
```

### Приватні властивості (#)

```js
class User {
    #password;
    constructor(name, password) {
        this.name = name;
        this.#password = password;
    }
    checkPassword(pw) {
        return this.#password === pw;
    }
}
```

#### Best practice

-   Використовуйте класи для складних структур.
-   Використовуйте приватні (#) властивості для інкапсуляції.
-   Додавайте jsdoc-коментарі для складних методів.

---

## Модулі та імпорт/експорт

### Експорт

```js
// math.js
export function add(a, b) {
    return a + b;
}
export const PI = 3.1415;
```

### Імпорт

```js
// app.js
import { add, PI } from "./math.js";
console.log(add(2, 3), PI);
```

### Експорт за замовчуванням

```js
// user.js
export default class User {
    /* ... */
}
// app.js
import User from "./user.js";
```

#### Best practice

-   Розділяйте код на модулі за функціоналом.
-   Іменуйте файли і модулі логічно.
-   Використовуйте сучасний синтаксис імпорту/експорту.

---

## Асинхронність: Promise, async/await

### Promise

```js
const fetchData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Дані отримано");
        }, 1000);
    });
};
fetchData().then((data) => console.log(data));
```

### async/await

```js
async function getData() {
    try {
        const data = await fetchData();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
getData();
```

### Promise.all / Promise.race

```js
const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
Promise.all([p1, p2]).then((values) => console.log(values)); // [1, 2]
Promise.race([p1, p2]).then((value) => console.log(value)); // 1
```

#### Best practice

-   Використовуйте async/await для читабельності.
-   Обробляйте помилки через try/catch.
-   Не ігноруйте відмову Promise.

---

## Робота з DOM

### Вибір елементів

```js
const btn = document.querySelector("#myBtn");
const items = document.querySelectorAll(".item");
```

### Маніпуляції

```js
btn.textContent = "Натисни мене!";
btn.classList.add("active");

btn.addEventListener("click", () => {
    alert("Кнопка натиснута!");
});
```

### Створення та видалення елементів

```js
const newDiv = document.createElement("div");
newDiv.textContent = "Новий елемент";
document.body.appendChild(newDiv);

document.body.removeChild(newDiv);
```

#### Best practice

-   Використовуйте сучасні селектори (`querySelector`, `querySelectorAll`).
-   Не маніпулюйте DOM надто часто — це впливає на продуктивність.
-   Організовуйте обробку подій через делегування (event delegation).

---

## Події

### Додавання обробника

```js
document.addEventListener("DOMContentLoaded", () => {
    console.log("Сторінка завантажена!");
});
```

### Event delegation

```js
document.querySelector(".list").addEventListener("click", (e) => {
    if (e.target.matches(".item")) {
        console.log("Клік по елементу:", e.target.textContent);
    }
});
```

### Властивості подій

```js
btn.addEventListener("click", (event) => {
    event.preventDefault(); // Зупинка стандартної дії
    event.stopPropagation(); // Зупинка поширення події
});
```

---

## Помилки та обробка винятків

### try/catch/finally

```js
try {
    const result = riskyOperation();
    console.log(result);
} catch (err) {
    console.error("Сталася помилка:", err);
} finally {
    console.log("Операція завершена!");
}
```

### Глобальна обробка помилок

```js
window.addEventListener("error", function (e) {
    console.error("Глобальна помилка:", e.message);
});
```

#### Best practice

-   Обробляйте помилки у асинхронному коді.
-   Додавайте користувацькі повідомлення для користувача.
-   Логгіруйте помилки для аналізу.

---

## Web APIs: Fetch, LocalStorage, Geolocation

### Fetch (AJAX-запити)

```js
fetch("https://api.example.com/data")
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error(error));
```

### async/await з fetch

```js
async function fetchData() {
    try {
        const resp = await fetch("https://api.example.com/data");
        const data = await resp.json();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

### LocalStorage

```js
localStorage.setItem("username", "Ivan");
const name = localStorage.getItem("username");
localStorage.removeItem("username");
```

### Geolocation

```js
navigator.geolocation.getCurrentPosition(
    (position) => console.log(position.coords),
    (error) => console.error(error)
);
```

---

## Сучасний синтаксис ES6+

### Стрілочні функції

```js
const add = (a, b) => a + b;
```

### Деструктуризація

```js
const user = { name: "Марія", age: 27 };
const { name, age } = user;
```

### Шаблонні рядки

```js
const greeting = `Вітаю, ${name}! Вам ${age} років.`;
```

### Короткий запис властивостей

```js
const x = 10,
    y = 20;
const point = { x, y }; // { x: 10, y: 20 }
```

### Spread & Rest оператори

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; // [1, 2, 3, 4]

function sum(...nums) {
    return nums.reduce((acc, n) => acc + n, 0);
}
```

### Модулі

```js
// import/export приклади у відповідній секції
```

### Приватні поля класу

```js
class User {
    #id = 123;
}
```

---

## Фреймворки та бібліотеки

### React

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);
    return (
        <button onClick={() => setCount(count + 1)}>Натиснуто: {count}</button>
    );
}
```

### Vue

```js
<template>
  <button @click="count++">Count: {{ count }}</button>
</template>
<script setup>
import { ref } from 'vue';
const count = ref(0);
</script>
```

### Next.js

-   Фреймворк для серверного рендерингу, сучасна маршрутизація.
-   [Офіційна документація](https://nextjs.org/docs)

### Svelte

-   Простий синтаксис, швидкий рендеринг.
-   [Офіційна документація](https://svelte.dev/docs)

---

## Best Practices

-   Використовуйте сучасний синтаксис ES6+.
-   Розділяйте код на логічні модулі.
-   Документуйте функції, особливо складні.
-   Використовуйте const/let, не var.
-   Не використовуйте застарілі API.
-   Дотримуйтеся одного стилю іменування.
-   Використовуйте eslint/prettier для автоматичної перевірки якості.
-   Обробляйте всі помилки.
-   Не забувайте про безпечне використання даних користувача.
-   Використовуйте делегування подій для оптимізації DOM.
-   Пишіть тестований код (наприклад, з Jest, Vitest).
-   Коментуйте нестандартні рішення.

---

## Типові помилки та їх уникнення

| Помилка                          | Як уникнути                                       |
| -------------------------------- | ------------------------------------------------- |
| Забули оголосити змінну          | Використовуйте `use strict` і сучасні інструменти |
| Використання var                 | Замініть на let/const                             |
| Відсутня обробка помилок         | Завжди обробляйте винятки try/catch               |
| Застарілий синтаксис             | Використовуйте ES6+                               |
| Дублювання коду                  | Виносьте повторювані частини у функції/модулі     |
| Зловживання глобальними змінними | Мінімізуйте область видимості                     |
| Відсутність перевірки типів      | Використовуйте TypeScript або JSDoc               |
| Неправильна робота з this        | Використовуйте стрілочні функції або bind         |
| Неправильні селектори DOM        | Перевіряйте валідність селектора                  |
| Маніпуляції DOM у циклі          | Використовуйте фрагменти або делегування          |

---

## FAQ

**Q: Чим відрізняється let, const та var?**  
A: `let` і `const` мають блочну область видимості, `var` — функціональну (і застарілий). `const` — для незмінних значень.

**Q: Як зробити запит до API?**  
A: Використовуйте `fetch`, async/await, обробляйте помилки.

**Q: Для чого потрібні проміси (Promise)?**  
A: Для роботи з асинхронними операціями, наприклад, завантаження даних.

**Q: Як структурувати великий проект?**  
A: За компонентами, модулями, з використанням сучасних фреймворків.

**Q: Чи варто використовувати TypeScript?**  
A: Так, для великих проєктів — він додає типізацію і зменшує кількість помилок.

**Q: Як оптимізувати продуктивність JS?**  
A: Мінімізуйте маніпуляції DOM, використовуйте делегування подій, оптимізуйте цикли.

**Q: Чи потрібно тестувати JS-код?**  
A: Так, використовуйте Jest, Vitest або інші сучасні фреймворки.

**Q: Які сучасні фреймворки найпопулярніші?**  
A: React, Next.js, Vue, Svelte.

---

## Корисні ресурси

-   [MDN Web Docs: JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
-   [ECMAScript 2024 Language Specification](https://tc39.es/ecma262/)
-   [JavaScript.info — сучасний туторіал](https://javascript.info/)
-   [ESLint — лінтер для якості коду](https://eslint.org/)
-   [Prettier — автоформатування коду](https://prettier.io/)
-   [Jest — тестування JS](https://jestjs.io/)
-   [Vite — сучасний збирач](https://vitejs.dev/)
-   [TypeScript — типізація JS](https://www.typescriptlang.org/)
-   [Node.js — серверний JavaScript](https://nodejs.org/)
-   [React — фреймворк для UI](https://react.dev/)
-   [Vue — сучасний фреймворк](https://vuejs.org/)
-   [Next.js — серверний рендеринг](https://nextjs.org/)
-   [Svelte — сучасний фреймворк](https://svelte.dev/)
-   [Vitest — сучасне тестування JS](https://vitest.dev/)

---

## Короткий підсумок

JavaScript — це основа сучасної веб-розробки. Важливо писати чистий, зрозумілий, структурований код, використовувати сучасний синтаксис (ES6+), розділяти код на модулі, обробляти помилки та тестувати додатки.  
JS має потужну екосистему, підтримує різноманітні стилі програмування та інтегрується з найпопулярнішими фреймворками.  
Дотримуйтесь кращих практик, вивчайте нові можливості і не забувайте про документацію — це ключ до ефективної роботи з JavaScript у 2024+ році!

---

<!-- Якщо потрібна поглиблена лекція по конкретній темі (наприклад, async/await, React, Next.js, TypeScript, Web APIs, тестування), просто напиши тему! -->
