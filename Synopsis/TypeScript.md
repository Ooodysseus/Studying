# TypeScript (TS): сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке TypeScript](#що-таке-typescript)
-   [Історія та роль TS](#історія-та-роль-ts)
-   [Встановлення та конфігурація](#встановлення-та-конфігурація)
-   [Основи синтаксису](#основи-синтаксису)
-   [Типи даних](#типи-даних)
-   [Інтерфейси та типи (interface, type)](#інтерфейси-та-типи-interface-type)
-   [Класи та об'єктно-орієнтоване програмування](#класи-та-обєктно-орієнтоване-програмування)
-   [Масиви та кортежі](#масиви-та-кортежі)
-   [Перерахування (enum)](#перерахування-enum)
-   [Функції та typing](#функції-та-typing)
-   [Generics (узагальнення)](#generics-узагальнення)
-   [Модулі та імпорт/експорт](#модулі-та-імпорт-експорт)
-   [Union, Intersection, Literal Types](#union-intersection-literal-types)
-   [Type Narrowing, Guards, Assertion](#type-narrowing-guards-assertion)
-   [Advanced Types: keyof, typeof, infer, mapped types](#advanced-types-keyof-typeof-infer-mapped-types)
-   [Type Inference (виведення типів)](#type-inference-виведення-типів)
-   [Decorators (декоратори)](#decorators-декоратори)
-   [Внутрішні механізми: типова система, трансляція, memory management](#внутрішні-механізми-типова-система-трансляція-memory-management)
-   [Підводні камені та глибокі концепції](#підводні-камені-та-глибокі-концепції)
-   [Інтеграція з React, Node.js, Express, Next.js, NestJS](#інтеграція-з-react-nodejs-express-nextjs-nestjs)
-   [Performance traps](#performance-traps)
-   [Best practices](#best-practices)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**TypeScript (TS)** — це надбудова над JavaScript, що додає статичну типізацію, розширені можливості ООП, generics, контроль типів на етапі компіляції, автоматичне рефакторування й інтеграцію з сучасними фреймворками. У 2024 році TS — стандарт для великих, масштабованих, підтримуваних проектів, від front-end до back-end (Node.js, NestJS, Next.js, React).

---

## Що таке TypeScript

TypeScript — мова програмування, що компілюється у чистий JavaScript. Додає типи, інтерфейси, generics, розширені можливості для роботи з великим кодом, підвищує безпеку та якість розробки.

-   **Статична типізація** — помилки виявляються ще до виконання коду.
-   **Сучасний синтаксис** — підтримка всіх ES6+ можливостей.
-   **Сумісність** — будь-який JS-код є валідним TS-кодом.

---

## Історія та роль TS

-   **2012:** Реліз TypeScript Microsoft.
-   **2015+:** Вибух популярності завдяки Angular 2+, React, Node.js.
-   **2024+:** TS — стандарт корпоративної розробки, основа для підтримки великих проектів, інтеграції з сучасними фреймворками.

---

## Встановлення та конфігурація

### Встановлення

```bash
npm install -g typescript
```

### Ініціалізація проекту

```bash
tsc --init
```

> Створює `tsconfig.json` — головний конфігураційний файл TypeScript.

#### Приклад базового tsconfig.json

```json
{
    "compilerOptions": {
        "target": "ES2022",
        "module": "ESNext",
        "strict": true,
        "esModuleInterop": true,
        "skipLibCheck": true,
        "forceConsistentCasingInFileNames": true,
        "outDir": "./dist"
    },
    "include": ["src"],
    "exclude": ["node_modules", "dist"]
}
```

---

## Основи синтаксису

### Оголошення типів

```typescript
let age: number = 25;
const name: string = "Олег";
let isAdmin: boolean = true;
```

### Функції з типами

```typescript
function greet(user: string): string {
    return `Привіт, ${user}!`;
}
```

### Необов'язкові параметри та дефолтні значення

```typescript
function log(msg: string, level: "info" | "warn" = "info") {
    console.log(`[${level}] ${msg}`);
}
```

---

## Типи даних

| Тип     | Приклад                |
| ------- | ---------------------- |
| number  | `5`, `3.14`            |
| string  | `"hello"`, `'world'`   |
| boolean | `true`, `false`        |
| array   | `string[]`, `number[]` |
| tuple   | `[string, number]`     |
| any     | `any`                  |
| unknown | `unknown`              |
| void    | `void`                 |
| never   | `never`                |
| object  | `{key: value}`         |
| enum    | `enum`                 |

#### Приклад масиву

```typescript
const skills: string[] = ["TS", "JS", "React"];
```

#### Кортеж

```typescript
const userInfo: [string, number] = ["Олена", 23];
```

---

## Інтерфейси та типи (interface, type)

### Інтерфейс

```typescript
interface User {
    id: number;
    name: string;
    isAdmin?: boolean; // необов'язковий
}
```

### Тип

```typescript
type Product = {
    id: number;
    name: string;
    price: number;
};
```

### Розширення інтерфейсів

```typescript
interface Admin extends User {
    permissions: string[];
}
```

### Union типи

```typescript
type Status = "pending" | "success" | "error";
```

---

## Класи та об'єктно-орієнтоване програмування

### Клас

```typescript
class Animal {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    speak(): string {
        return `${this.name} каже "Привіт!"`;
    }
}
```

### Наслідування

```typescript
class Dog extends Animal {
    bark(): string {
        return `${this.name} гавкає`;
    }
}
```

### Інтерфейс для класу

```typescript
interface Movable {
    move(distance: number): void;
}
class Car implements Movable {
    move(distance: number) {
        console.log(`Авто проїхало ${distance} км.`);
    }
}
```

---

## Масиви та кортежі

### Масиви

```typescript
const points: number[] = [10, 20, 30];
```

### Кортежі

```typescript
const userTuple: [string, number, boolean] = ["Олег", 25, true];
```

---

## Перерахування (enum)

```typescript
enum Role {
    User = "USER",
    Admin = "ADMIN",
    Guest = "GUEST",
}
const myRole: Role = Role.Admin;
```

---

## Функції та typing

### Вказання типів для аргументів і повернення

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

### Функції з необов'язковими та дефолтними параметрами

```typescript
function multiply(a: number, b?: number): number {
    return a * (b ?? 1);
}
```

### Arrow-функції

```typescript
const sum = (a: number, b: number): number => a + b;
```

---

## Generics (узагальнення)

### Простий generic

```typescript
function identity<T>(value: T): T {
    return value;
}
identity<number>(42);
identity<string>("hello");
```

### Generic interface

```typescript
interface ApiResponse<T> {
    data: T;
    error?: string;
}
```

### Generic class

```typescript
class Box<T> {
    content: T;
    constructor(value: T) {
        this.content = value;
    }
}
```

---

## Модулі та імпорт/експорт

### Експорт

```typescript
export interface User {
    id: number;
    name: string;
}
export const defaultUser: User = { id: 0, name: "Гість" };
```

### Імпорт

```typescript
import { User, defaultUser } from "./user";
```

---

## Union, Intersection, Literal Types

### Union

```typescript
type Status = "success" | "error" | "pending";
```

### Intersection

```typescript
type Admin = User & { permissions: string[] };
```

### Literal Types

```typescript
type Direction = "left" | "right" | "up" | "down";
```

---

## Type Narrowing, Guards, Assertion

### Type Narrowing

```typescript
function printId(id: number | string) {
    if (typeof id === "string") {
        console.log(id.toUpperCase());
    } else {
        console.log(id);
    }
}
```

### Type Guards

```typescript
interface Fish {
    swim(): void;
}
interface Bird {
    fly(): void;
}

function isFish(animal: Fish | Bird): animal is Fish {
    return (animal as Fish).swim !== undefined;
}
```

### Type Assertion

```typescript
const input = document.getElementById("username") as HTMLInputElement;
console.log(input.value);
```

---

## Advanced Types: keyof, typeof, infer, mapped types

### keyof

```typescript
type UserKeys = keyof User; // 'id' | 'name' | 'isAdmin'
```

### typeof

```typescript
const user = { id: 1, name: "Олег" };
type UserType = typeof user;
```

### infer (в умовних типах)

```typescript
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;
```

### Mapped Types

```typescript
type ReadonlyUser = { readonly [K in keyof User]: User[K] };
```

---

## Type Inference (виведення типів)

TypeScript часто самостійно визначає тип змінної, функції чи властивості.

```typescript
let price = 150; // price: number
const items = ["Apple", "Banana"]; // items: string[]
```

---

## Decorators (декоратори)

> Декоратори — експериментальна можливість (2024+), активно використовуються в NestJS, Angular.

```typescript
function Log(target: any, key: string) {
    let value = target[key];
    const getter = () => {
        console.log(`Отримання ${key}: ${value}`);
        return value;
    };
    Object.defineProperty(target, key, { get: getter });
}

class Product {
    @Log
    price: number = 100;
}
```

---

## Внутрішні механізми: типова система, трансляція, memory management

-   **Типова система TS** — працює лише на етапі компіляції, у рантаймі всі типи зникають.
-   **Transpilation** — TypeScript компілюється у чистий JavaScript, відповідно до налаштувань (target: ES2022+).
-   **Memory management** — на рівні рантайму керується JavaScript-движком (V8, SpiderMonkey).

#### Схема трансляції

```
TypeScript (.ts) → Transpilation → JavaScript (.js) → Виконання в JS-движку
```

---

## Підводні камені та глибокі концепції

### Type vs Interface

-   `type` — може описувати примітиви, union/intersection, mapped types.
-   `interface` — призначений для опису об'єктів, класів, може розширюватись.

### any vs unknown

-   `any` — знімає всю перевірку типів (небезпечно).
-   `unknown` — безпечніший, потрібно явно перевіряти тип.

### Strict режим

-   Включай `"strict": true` у tsconfig для максимальної типізації.

### Type erasure

-   Всі типи видаляються на етапі компіляції — у рантаймі їх немає!

### Deep dive посилання

-   [Understanding TypeScript’s type system](https://www.typescriptlang.org/docs/handbook/type-system.html)
-   [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)

---

## Інтеграція з React, Node.js, Express, Next.js, NestJS

### React + TypeScript

```tsx
interface Props {
    title: string;
    count?: number;
}
const Counter: React.FC<Props> = ({ title, count = 0 }) => (
    <div>
        <h2>{title}</h2>
        <p>{count}</p>
    </div>
);
```

### Next.js + TypeScript

```tsx
// pages/index.tsx
import type { NextPage } from "next";
const Home: NextPage = () => <h1>Головна!</h1>;
export default Home;
```

### Node.js + Express + TypeScript

```typescript
import express, { Request, Response } from "express";
const app = express();

app.get("/api", (req: Request, res: Response) => {
    res.json({ message: "API працює!" });
});
```

### NestJS + TypeScript (Decorator)

```typescript
import { Controller, Get } from "@nestjs/common";

@Controller("users")
export class UsersController {
    @Get()
    findAll() {
        return ["Олег", "Олена"];
    }
}
```

---

## Performance traps

-   **Велика кількість any** — знижує користь TS.
-   **Застарілі декларації типів** — можуть призводити до помилок.
-   **Неправильна інтеграція з бібліотеками** — декларації типів можуть бути неактуальними.
-   **Дублювання типів** — складність підтримки, ризик розбіжностей.

---

## Best practices

-   Завжди використовуй `"strict": true` у tsconfig
-   Віддавай перевагу `unknown` замість `any`
-   Мінімізуй дублювання типів
-   Винось типи у окремі файли/модулі
-   Використовуй інтерфейси для класів, типи для union/intersection
-   Додавай типи для всіх аргументів та повернення функцій
-   Використовуй generics для гнучкості типів
-   Завжди оновлюй @types для сторонніх бібліотек
-   Рефактори код для зменшення any/implicit types
-   Тестуй типи через unit-тести (Jest/ts-jest/Vitest)
-   Валідуй типи при інтеграції з API

---

## Корисні ресурси та документація

-   [TypeScript Official Docs](https://www.typescriptlang.org/docs/)
-   [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
-   [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
-   [DefinitelyTyped (@types)](https://github.com/DefinitelyTyped/DefinitelyTyped)
-   [React + TS Docs](https://react.dev/learn/typescript)
-   [Next.js + TS Docs](https://nextjs.org/docs/pages/building-your-application/configuring/typescript)
-   [NestJS Docs](https://docs.nestjs.com/)
-   [Awesome TypeScript](https://github.com/dzharii/awesome-typescript)
-   [TypeScript Playground](https://www.typescriptlang.org/play)
-   [MDN TypeScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError)

---

## Короткий підсумок

**TypeScript — це основа сучасної розробки для великих web та server-side проектів у 2024 році.**  
Статична типізація, generics, interface/type, розширені механізми, інтеграція з популярними фреймворками — це ключ до безпечного, масштабованого й підтримуваного коду.  
Дотримуйся best practices, регулярно оновлюй знання, інтегруй TS у свої проекти та використовуй офіційну документацію для глибокого занурення!

---
