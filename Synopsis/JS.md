# Ultimate JavaScript Cheat Sheet

## ⭐ Description

JavaScript (JS) is a versatile, interpreted language for web, server, and desktop development. It enables interactivity, logic, and data manipulation in browsers and powers backends via Node.js. It's the basis for frameworks like Vue, Angular, and Electron.

## ⭐ Relationship With Other Technologies

-   HTML: JS manipulates HTML structure via the DOM.
-   CSS/SCSS: JS can change CSS styles dynamically.
-   TypeScript: TS is JS with types.
-   Vue/Angular/Nuxt/Electron: JS is used for logic, components, and interactivity.
-   Node/Express: JS is used for server-side programming.
-   Django/Python: Python is used server-side, but JS runs in browsers.
-   Electron: JS powers desktop app logic.

---

## 1. Variables & Data Types

```js
let x = 5; // Block-scoped
const y = 10; // Constant
var z = "test"; // Function-scoped, legacy

// Data types
let num = 42; // Number
let str = "Hello"; // String
let bool = true; // Boolean
let arr = [1, 2, 3]; // Array
let obj = { name: "John" }; // Object
let nul = null; // Null
let und = undefined; // Undefined
let sym = Symbol("desc"); // Symbol
let big = 123n; // BigInt
```

---

## 2. Operators

-   Arithmetic: `+`, `-`, `*`, `/`, `%`, `**`
-   Assignment: `=`, `+=`, `-=`, `*=`, `/=`
-   Comparison: `==`, `===`, `!=`, `!==`, `<`, `>`, `<=`, `>=`
-   Logical: `&&`, `||`, `!`
-   Ternary: `condition ? expr1 : expr2`
-   Spread: `[...arr]`
-   Rest: `function(...args) {}`

---

## 3. Functions

```js
function add(a, b) {
    return a + b;
}
const sub = (a, b) => a - b;
const sum = function (a, b) {
    return a + b;
};
(function () {
    /* IIFE */
})();
```

---

## 4. Control Flow

```js
if (x > 10) { ... }
else if (x > 5) { ... }
else { ... }

for (let i = 0; i < 10; i++) { ... }
while (condition) { ... }
do { ... } while (condition);

switch (value) {
  case 1: ...; break;
  default: ...;
}
```

---

## 5. Arrays & Objects

### Arrays

```js
let arr = [1, 2, 3];
arr.push(4);
arr.pop();
arr.shift();
arr.unshift(0);
arr.map((x) => x * 2);
arr.filter((x) => x > 2);
arr.reduce((a, b) => a + b, 0);
arr.slice(1, 3);
arr.splice(1, 1);
arr.find((x) => x === 2);
```

### Objects

```js
let obj = { name: "John", age: 30 };
obj.name;
obj["age"];
Object.keys(obj);
Object.values(obj);
Object.entries(obj);
Object.assign({}, obj, { age: 31 });
```

---

## 6. ES6+ Features

-   Arrow Functions: `(x) => x * x`
-   Template Literals: `` `Hello ${name}` ``
-   Destructuring: `const {a, b} = obj;`
-   Spread/Rest: `[...arr]`, `function(...args)`
-   Default Parameters: `function(x = 1) {}`
-   Classes: `class MyClass { ... }`
-   Modules: `import`, `export`
-   Optional Chaining: `obj?.prop?.subprop`
-   Nullish Coalescing: `x ?? 'default'`

---

## 7. Classes & OOP

```js
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        console.log(`${this.name} speaks.`);
    }
}
class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks.`);
    }
}
let dog = new Dog("Rex");
dog.speak();
```

---

## 8. DOM Manipulation

```js
document.getElementById("id");
document.querySelector(".class");
element.innerHTML = "New Content";
element.style.color = "blue";
element.classList.add("active");
element.setAttribute("data-id", "123");
element.remove();
```

---

## 9. Events

```js
button.addEventListener('click', (e) => { ... });
document.addEventListener('DOMContentLoaded', () => { ... });
```

---

## 10. Async / Await & Promises

```js
const p = new Promise((resolve, reject) => { ... });
p.then(result => { ... }).catch(err => { ... });

async function fetchData() {
  const res = await fetch('/api');
  const data = await res.json();
  return data;
}
```

---

## 11. Error Handling

```js
try {
    throw new Error("Oops");
} catch (e) {
    console.error(e.message);
} finally {
    // Always runs
}
```

---

## 12. Regular Expressions

```js
const re = /\d+/g;
"abc123".match(re);
```

---

## 13. Local Storage, Session Storage & Cookies

```js
localStorage.setItem("key", "value");
localStorage.getItem("key");
sessionStorage.setItem("key", "value");
document.cookie = "user=John; expires=Thu, 18 Dec 2025 12:00:00 UTC";
```

---

## 14. Fetch API & AJAX

```js
fetch("https://api.example.com/data")
    .then((res) => res.json())
    .then((json) => console.log(json));

const xhr = new XMLHttpRequest();
xhr.open("GET", "/api");
xhr.onload = () => {
    console.log(xhr.responseText);
};
xhr.send();
```

---

## 15. Modules

```js
// file: math.js
export function add(a, b) {
    return a + b;
}
export default function sub(a, b) {
    return a - b;
}

// file: main.js
import { add } from "./math.js";
import sub from "./math.js";
```

---

## 16. Advanced Patterns

-   **Debounce/Throttle:** Control event firing rate.
-   **Currying:** `const curried = a => b => c => a + b + c;`
-   **Memoization:** Cache function results.

---

## 17. Best Practices

-   Use `let`/`const`, avoid `var`.
-   Modularize code using functions/classes/modules.
-   Always handle errors.
-   Use strict mode: `'use strict';`
-   Use linters (ESLint) and formatters (Prettier).
-   Prefer functional programming for clarity.
-   Avoid polluting global scope.

---

## 18. Tools & Resources

-   [MDN JS Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
-   [ESLint](https://eslint.org/)
-   [Prettier](https://prettier.io/)
-   [Node.js](https://nodejs.org/)
-   [JSFiddle](https://jsfiddle.net/)
-   [Can I use](https://caniuse.com/)

---

## 19. Interoperability Table

| Feature           | JS  | HTML | CSS/SCSS | TS  | Vue/Angular/Nuxt | Node/Express | Django/Python | Electron |
| ----------------- | --- | ---- | -------- | --- | ---------------- | ------------ | ------------- | -------- |
| Logic/Behavior    | ✔️  |      |          | ✔️  | ✔️               | ✔️           |               | ✔️       |
| DOM Manipulation  | ✔️  | ✔️   | ✔️       | ✔️  | ✔️               |              |               | ✔️       |
| Desktop App Logic | ✔️  | ✔️   | ✔️       | ✔️  |                  |              |               | ✔️       |
