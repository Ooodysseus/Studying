# JavaScript (JS): сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке JavaScript](#що-таке-javascript)
-   [Історія та ролі JS](#історія-та-ролі-js)
-   [Сучасний синтаксис (ES6+)](#сучасний-синтаксис-es6)
-   [Типи даних](#типи-даних)
-   [Змінні, let/const/var, scope та hoisting](#змінні-let-const-var-scope-та-hoisting)
-   [Оператори](#оператори)
-   [Функції: декларація, стрілочні, замикання](#функції-декларація-стрілочні-замикання)
-   [Об'єкти та класи](#об'єкти-та-класи)
-   [Масиви та методи роботи з ними](#масиви-та-методи-роботи-з-ними)
-   [Деструктуризація, spread, rest](#деструктуризація-spread-rest)
-   [Модулі та імпорт/експорт](#модулі-та-імпорт-експорт)
-   [Promise, async/await, Event Loop](#promise-async-await-event-loop)
-   [Замикання (Closure)](#замикання-closure)
-   [Внутрішні механізми: прототипи, prototype chain, this](#внутрішні-механізми-прототипи-prototype-chain-this)
-   [Garbage Collection та управління пам'яттю](#garbage-collection-та-управління-памяттю)
-   [Error handling, try/catch, custom errors](#error-handling-trycatch-custom-errors)
-   [DOM та взаємодія з HTML](#dom-та-взаємодія-з-html)
-   [Event delegation, bubbling, capturing](#event-delegation-bubbling-capturing)
-   [Масштабованість та тестування](#масштабованість-та-тестування)
-   [Security traps: XSS, CSRF, eval](#security-traps-xss-csrf-eval)
-   [Performance traps та оптимізація](#performance-traps-та-оптимізація)
-   [Сучасні фреймворки: React, Vue, Angular](#сучасні-фреймворки-react-vue-angular)
-   [Best practices](#best-practices)
-   [Корисні ресурси](#корисні-ресурси)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**JavaScript (JS)** — це найпопулярніша мова програмування для web-розробки, яка забезпечує динамічність, інтерактивність, логіку й зв'язок із backend.  
У 2024+ JS — це не лише браузер, а й сервер (Node.js), мобільні додатки (React Native), десктоп (Electron), embedded (Espruino), AI, automation та ще більше.

---

## Що таке JavaScript

JavaScript — це високорівнева, інтерпретована, мультипарадигмова мова програмування, спроектована для взаємодії з DOM, обробки подій, роботи з мережами та даними.  
JS — єдина мова, яку розуміє кожен браузер.

---

## Історія та ролі JS

-   **1995:** Створено Brendan Eich для Netscape.
-   **1997:** ECMAScript — стандарт для JS.
-   **2015 (ES6+):** Революція в синтаксисі, появa класів, стрілочних функцій, модулів, промісів, async/await.
-   **2024+:** JS — універсальний рушій для фронтенду, бекенду, автоматизації, AI (TensorFlow.js), сучасна SPA/SSR/SSG, Web Components.

---

## Сучасний синтаксис (ES6+)

```js
// Стрілочна функція
const sum = (a, b) => a + b;

// Деструктуризація
const { name, age } = user;

// Клас
class User {
    constructor(name) {
        this.name = name;
    }
    greet() {
        return `Вітаю, ${this.name}!`;
    }
}
```

---

## Типи даних

| Тип       | Приклад                           |
| --------- | --------------------------------- |
| Number    | `42`, `3.14`                      |
| String    | `"hello"`, `'js'`                 |
| Boolean   | `true`, `false`                   |
| Undefined | `undefined`                       |
| Null      | `null`                            |
| Object    | `{ key: value }`                  |
| Array     | `[1, 2, 3]`                       |
| Symbol    | `Symbol('id')`                    |
| BigInt    | `123456789012345678901234567890n` |

#### Перевірка типу

```js
typeof 42; // "number"
typeof null; // "object" (особливість JS)
```

---

## Змінні let/const/var, scope та hoisting

-   **let** — блочна область видимості, можна змінювати
-   **const** — блочна область видимості, не можна переназначати
-   **var** — функціональна область видимості, застаріле

### Scope (область видимості)

-   Глобальна
-   Функціональна
-   Блочна

#### Приклад

```js
let x = 10;
if (true) {
    let x = 20; // локальна змінна
}
console.log(x); // 10
```

### Hoisting (підняття)

-   Змінні `var` і функції піднімаються на початок області
-   `let`/`const` — не піднімаються, виникає "temporal dead zone"

#### Приклад

```js
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError
let b = 6;
```

---

## Оператори

-   Арифметичні: `+`, `-`, `*`, `/`, `%`, `**`
-   Порівняння: `==`, `===`, `!=`, `!==`, `<`, `>`, `<=`, `>=`
-   Логічні: `&&`, `||`, `!`
-   Присвоєння: `=`, `+=`, `-=`, `*=`, `/=`
-   Тернарний: `умова ? якщо_так : якщо_ні`
-   Spread/Rest: `...`
-   Nullish coalescing: `??`

#### Приклад

```js
const result = isValid ? "ОК" : "Помилка";
const arr = [1, 2, ...otherArr];
```

---

## Функції: декларація, стрілочні, замикання

### Оголошення функції

```js
function greet(name) {
    return `Привіт, ${name}`;
}
```

### Стрілочна функція

```js
const greet = (name) => `Привіт, ${name}`;
```

### Замикання (Closure)

```js
function makeCounter() {
    let count = 0;
    return function () {
        count++;
        return count;
    };
}
const counter = makeCounter();
counter(); // 1
counter(); // 2
```

> Замикання дозволяють зберігати стан усередині функції.

---

## Об'єкти та класи

### Об'єкт

```js
const user = {
    name: "Андрій",
    age: 22,
    greet() {
        return `Вітаю, ${this.name}!`;
    },
};
```

### Клас (ES6+)

```js
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        return `${this.name} каже "Привіт!"`;
    }
}
const cat = new Animal("Мурчик");
cat.speak(); // Мурчик каже "Привіт!"
```

### Наслідування

```js
class Dog extends Animal {
    bark() {
        return `${this.name} гавкає`;
    }
}
```

---

## Масиви та методи роботи з ними

### Основні методи

-   `push`, `pop`, `shift`, `unshift`
-   `map`, `filter`, `reduce`, `find`, `some`, `every`, `includes`
-   `sort`, `reverse`, `slice`, `splice`

#### Приклад

```js
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((n) => n * 2); // [2, 4, 6, 8]
const evens = numbers.filter((n) => n % 2 === 0); // [2, 4]
const sum = numbers.reduce((acc, n) => acc + n, 0); // 10
```

---

## Деструктуризація, spread, rest

### Деструктуризація

```js
const user = { name: "Олена", age: 27 };
const { name, age } = user;

const arr = [10, 20, 30];
const [first, ...rest] = arr;
```

### Spread

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3, 4]; // [1, 2, 3, 4]
```

### Rest

```js
function sum(...args) {
    return args.reduce((acc, n) => acc + n, 0);
}
```

---

## Модулі та імпорт/експорт

### Експорт

```js
export function greet(name) {
    return `Привіт, ${name}`;
}
```

### Імпорт

```js
import { greet } from "./utils.js";
```

-   Стандартний модульний синтаксис (ESM) підтримується у всіх сучасних браузерах та Node.js з 2022+.

---

## Promise, async/await, Event Loop

### Promise

```js
const fetchData = () =>
    new Promise((resolve, reject) => {
        setTimeout(() => resolve("Дані отримані!"), 1000);
    });

fetchData().then((data) => console.log(data));
```

### Async/Await

```js
async function getData() {
    const data = await fetchData();
    console.log(data);
}
```

### Event Loop

-   **Event loop** — механізм JS, що забезпечує асинхронність.
-   Основні черги: call stack, task queue, microtask queue.

#### Схема

```
+------------------+
| Call Stack       |
|------------------|
| Microtasks Queue |
|------------------|
| Tasks Queue      |
+------------------+
```

#### Приклад асинхронності

```js
console.log("A");
setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));
console.log("D");
// Вивід: A D C B
```

---

## Замикання (Closure)

**Closure** — це функція, що має доступ до змінних з зовнішньої області видимості, навіть після завершення цієї області.

#### Приклад

```js
function multiplier(factor) {
    return function (number) {
        return number * factor;
    };
}
const double = multiplier(2);
double(5); // 10
```

---

## Внутрішні механізми: прототипи, prototype chain, this

### Прототипи та prototype chain

-   Кожен об'єкт має прототип (`[[Prototype]]`)
-   Ланцюжок прототипів — основа наслідування

#### Приклад

```js
function Person(name) {
    this.name = name;
}
Person.prototype.greet = function () {
    return `Привіт, ${this.name}`;
};
const p = new Person("Олег");
p.greet(); // Привіт, Олег
```

#### Схема prototype chain

```
p --> Person.prototype --> Object.prototype --> null
```

### this

-   Вказує на об'єкт у контексті виклику функції
-   В Arrow Functions — береться із зовнішнього контексту

#### Приклад

```js
const user = {
    name: "Олег",
    show: function () {
        return this.name;
    },
    showArrow: () => this.name, // undefined, бо arrow бере з глобального
};
```

---

## Garbage Collection та управління пам'яттю

-   JS має автоматичний garbage collector (V8, SpiderMonkey)
-   Видаляє об'єкти, до яких немає посилань
-   Слід уникати memory leaks (наприклад, глобальних змінних, незакритих event listeners)

#### Приклад memory leak

```js
let arr = [];
setInterval(() => arr.push(new Array(1000000)), 1000); // пам'ять зростає без очищення
```

---

## Error handling, try/catch, custom errors

### try/catch

```js
try {
    throw new Error("Щось пішло не так!");
} catch (err) {
    console.error(err.message);
}
```

### Custom Error

```js
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}
throw new ValidationError("Невалідні дані!");
```

### finally

```js
try {
    // ...
} catch (err) {
    // ...
} finally {
    // завжди виконається
}
```

---

## DOM та взаємодія з HTML

### Вибір елементів

```js
const title = document.querySelector("h1");
title.textContent = "Новий заголовок";
```

### Маніпуляція класами

```js
title.classList.add("active");
```

### Додавання елементів

```js
const btn = document.createElement("button");
btn.textContent = "Натисни мене";
document.body.appendChild(btn);
```

---

## Event delegation, bubbling, capturing

### Делегування подій

```js
document.body.addEventListener("click", (e) => {
    if (e.target.matches(".btn")) {
        console.log("Клік по кнопці");
    }
});
```

### Bubbling та Capturing

-   Події спочатку рухаються вниз (capturing), потім вгору (bubbling)

```js
element.addEventListener("click", handler, true); // capturing
element.addEventListener("click", handler, false); // bubbling
```

#### Схема

```
window
  ↘
document
  ↘
body
  ↘
div
  ↘
button
```

---

## Масштабованість та тестування

-   JS-код варто розбивати на модулі
-   Використовуй TypeScript для типізації
-   Для тестування: Jest, Vitest, Mocha, Cypress

#### Приклад Jest

```js
// greet.js
export const greet = (name) => `Привіт, ${name}`;

// greet.test.js
import { greet } from "./greet";
test("greet працює коректно", () => {
    expect(greet("Олег")).toBe("Привіт, Олег");
});
```

---

## Security traps: XSS, CSRF, eval

-   **XSS (Cross-site Scripting):** не вставляй дані напряму у DOM
-   **CSRF (Cross-site Request Forgery):** використовуй токени для захисту
-   **Eval:** не використовуй `eval()`, це небезпечно

#### Приклад XSS

```js
// Небезпечно!
element.innerHTML = userInput; // може бути код
```

#### Захист

-   Використовуй `textContent` замість `innerHTML`
-   Валідуй дані на сервері

---

## Performance traps та оптимізація

-   Зменшуй кількість DOM-операцій
-   Дебаунс/Throttle для подій скролу/ресайзу
-   Використовуй Web Workers для важких задач
-   Lazy loading для ресурсів

#### Приклад debounce

```js
function debounce(fn, delay) {
    let timeout;
    return (...args) => {
        clearTimeout(timeout);
        timeout = setTimeout(() => fn(...args), delay);
    };
}
window.addEventListener(
    "resize",
    debounce(() => {
        // код тут...
    }, 200)
);
```

---

## Сучасні фреймворки: React, Vue, Angular

### React

```jsx
import { useState } from "react";
function Counter() {
    const [count, setCount] = useState(0);
    return (
        <button onClick={() => setCount(count + 1)}>Лічильник: {count}</button>
    );
}
```

### Vue

```vue
<template>
    <button @click="count++">Лічильник: {{ count }}</button>
</template>
<script setup>
import { ref } from "vue";
const count = ref(0);
</script>
```

### Angular

```typescript
@Component({
    selector: "app-counter",
    template: `<button (click)="count++">Лічильник: {{ count }}</button>`,
})
export class CounterComponent {
    count = 0;
}
```

---

## Best practices

-   Використовуй `const` для незмінних змінних, `let` — для змінних
-   Використовуй сучасний синтаксис (ES6+)
-   Розділяй код на модулі та компоненти
-   Уникай глобальних змінних
-   Не використовуй застарілий синтаксис (`var`, `function` declaration у глобальному коді)
-   Валідуй і санітайз дані
-   Тестуй код (Unit, Integration, E2E)
-   Відповідно документуй код та API
-   Дотримуйся стандартів безпеки

---

## Корисні ресурси

-   [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
-   [ECMAScript Spec (ECMA-262)](https://tc39.es/ecma262/)
-   [JavaScript.info](https://javascript.info/)
-   [Node.js Documentation](https://nodejs.org/en/docs/)
-   [React Docs](https://react.dev/)
-   [Vue Docs](https://vuejs.org/)
-   [Angular Docs](https://angular.io/docs)
-   [Jest Docs](https://jestjs.io/docs/getting-started)
-   [TypeScript Docs](https://www.typescriptlang.org/docs/)
-   [Security: OWASP JS Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/JavaScript_Security_Cheat_Sheet.html)
-   [V8 Internals](https://v8.dev/docs)

---

## Короткий підсумок

**JavaScript — це серце сучасної web-розробки.**  
Глибоке розуміння внутрішніх механізмів (event loop, closure, prototype chain, memory management, performance traps) допоможе писати безпечний, швидкий, масштабований та підтримуваний код.  
Дотримуйся best practices, тестуй, слідкуй за новими можливостями й розвивайся разом із сучасним JavaScript!

---
