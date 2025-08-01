# Node.js: сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке Node.js](#що-таке-nodejs)
-   [Історія та роль Node.js](#історія-та-роль-nodejs)
-   [Встановлення та старт проекту](#встановлення-та-старт-проекту)
-   [Структура та організація проекту](#структура-та-організація-проекту)
-   [Модульна система: ESM vs CommonJS](#модульна-система-esm-vs-commonjs)
-   [Event Loop, асинхронність, Callback, Promise, async/await](#event-loop-асинхронність-callback-promise-asyncawait)
-   [Внутрішні механізми: Event Loop, V8, memory management, performance traps](#внутрішні-механізми-event-loop-v8-memory-management-performance-traps)
-   [Файлова система (fs), потоки (streams), Buffer](#файлова-система-fs-потоки-streams-buffer)
-   [HTTP сервер, Express, Fastify, Hono](#http-сервер-express-fastify-hono)
-   [Роутінг, middleware, обробка запитів](#роутінг-middleware-обробка-запитів)
-   [Робота з базами даних (MongoDB, PostgreSQL, Prisma, Mongoose)](#робота-з-базами-даних-mongodb-postgresql-prisma-mongoose)
-   [Авторизація, безпека, JWT, OAuth2, CSRF, Helmet](#авторизація-безпека-jwt-oauth2-csrf-helmet)
-   [Тестування (Jest, Vitest, Supertest, Mocha)](#тестування-jest-vitest-supertest-mocha)
-   [TypeScript у Node.js](#typescript-у-nodejs)
-   [Поглиблено: підкапотна робота Node.js (Event Loop, Streams, V8, GC, performance traps)](#поглиблено-підкапотна-робота-nodejs)
-   [Типові підводні камені, security traps](#типові-підводні-камені-security-traps)
-   [Best practices](#best-practices)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**Node.js** — це асинхронне середовище виконання JavaScript поза браузером, побудоване на рушії V8 (Google).  
У 2024 році Node.js — стандарт для серверної розробки: REST API, мікросервіси, real-time додатки, CLI, DevOps, serverless та cloud-native архітектури.

---

## Що таке Node.js

-   **Node.js** — це JavaScript runtime для серверного коду.
-   Побудований на основі V8 (Google Chrome JS Engine).
-   Має неблокуючу (non-blocking), асинхронну модель I/O.
-   Підходить для scalable, high-load додатків, real-time, мікросервісів.

---

## Історія та роль Node.js

-   **2009:** Старт Node.js (Ryan Dahl).
-   **2012–2016:** npm, Express, розквіт екосистеми.
-   **2018+:** ES Modules, async/await, microservices, serverless.
-   **2024+:** Node.js — основа для API, WebSocket, DevOps, JAMstack, serverless, cloud-native.

---

## Встановлення та старт проекту

### Встановлення через nvm (Node Version Manager)

```bash
nvm install --lts
nvm use --lts
```

### Створення проекту

```bash
mkdir node-app
cd node-app
npm init -y
```

### Встановлення Express

```bash
npm install express
```

---

## Структура та організація проекту

```
node-app/
├─ src/
│  ├─ index.js
│  ├─ routes/
│  ├─ controllers/
│  ├─ models/
│  ├─ middlewares/
│  └─ utils/
├─ tests/
├─ package.json
├─ .env
├─ .gitignore
```

-   Дотримуйся модульності (розділяй логіку на контролери, сервіси, моделі).
-   Використовуй сучасні фреймворки (Express, Fastify, Hono).

---

## Модульна система: ESM vs CommonJS

-   Node.js підтримує **CommonJS** (`require/module.exports`) та **ESM** (`import/export`).
-   У 2024+ році — рекомендується **ESM**.

### CommonJS

```js
// utils/math.js
module.exports.add = (a, b) => a + b;
```

```js
// index.js
const math = require("./utils/math");
console.log(math.add(2, 3));
```

### ES Modules (ESM)

```js
// utils/math.mjs
export const add = (a, b) => a + b;
```

```js
// index.mjs
import { add } from "./utils/math.mjs";
console.log(add(2, 3));
```

-   Для ESM: в package.json додай `"type": "module"`.

---

## Event Loop, асинхронність, Callback, Promise, async/await

-   Node.js працює на **Event Loop** — неблокуючий цикл обробки подій.
-   Асинхронність = продуктивність.

### Callback

```js
const fs = require("fs");
fs.readFile("file.txt", (err, data) => {
    if (err) throw err;
    console.log(data.toString());
});
```

### Promise

```js
const fs = require("fs/promises");
fs.readFile("file.txt", "utf8")
    .then((data) => console.log(data))
    .catch((err) => console.error(err));
```

### async/await

```js
const fs = require("fs/promises");
async function read() {
    try {
        const data = await fs.readFile("file.txt", "utf8");
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
read();
```

---

## Внутрішні механізми: Event Loop, V8, memory management, performance traps

### Event Loop

-   Node.js Event Loop — цикл, що обробляє tasks, microtasks, timers, I/O.
-   Асинхронність через thread pool (libuv).

#### Схема Event Loop

```
[call stack] <-> [event queue] <-> [event loop] <-> [libuv thread pool]
```

### V8 Engine

-   JS виконується через V8 (JIT compilation, оптимізація).
-   Garbage Collection — автоматичне очищення пам'яті.

### Performance traps

-   **Blocking code:** Не блокуйте event loop (sync I/O, великі обчислення).
-   **Memory leaks:** Слідкуйте за замиканнями, глобальними змінними.
-   **Callback hell:** Використовуйте async/await, Promise.

#### Deep dive

-   [Node.js Event Loop Guide](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)
-   [V8 Docs](https://v8.dev/)
-   [Node.js Performance Best Practices](https://nodejs.org/en/docs/guides/best-practices/)

---

## Файлова система (fs), потоки (streams), Buffer

### Файлова система (fs)

-   Робота з файлами: читання, запис, зміна.

```js
const fs = require("fs");
fs.writeFile("file.txt", "Hello Node.js!", (err) => {
    if (err) throw err;
});
```

### Потоки (streams)

-   Для великих файлів, мережевих операцій.

```js
const fs = require("fs");
const readStream = fs.createReadStream("bigfile.txt");
readStream.on("data", (chunk) => console.log("Частина:", chunk.length));
```

### Buffer

-   Робота з двійковими даними.

```js
const buf = Buffer.from("Node.js");
console.log(buf.toString("hex")); // 4e6f64652e6a73
```

---

## HTTP сервер, Express, Fastify, Hono

### HTTP Server (без фреймворків)

```js
const http = require("http");
http.createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello Node.js!");
}).listen(3000);
```

### Express

```js
import express from "express";
const app = express();
app.get("/", (req, res) => res.send("Hello Express!"));
app.listen(3000);
```

### Fastify

```js
import Fastify from "fastify";
const fastify = Fastify();
fastify.get("/", async (request, reply) => "Hello Fastify!");
fastify.listen({ port: 3000 });
```

### Hono (2024+)

```js
import { Hono } from "hono";
const app = new Hono();
app.get("/", (c) => c.text("Hello Hono!"));
app.fire();
```

---

## Роутінг, middleware, обробка запитів

-   Роутінг — розподіл запитів по шляхах.
-   Middleware — функції між запитом і відповіддю (логування, авторизація, body parsing).

### Express Middleware

```js
app.use(express.json());
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
});
```

### Fastify Middleware (Hooks)

```js
fastify.addHook("onRequest", async (request, reply) => {
    // логування запиту
});
```

---

## Робота з базами даних (MongoDB, PostgreSQL, Prisma, Mongoose)

### MongoDB (Mongoose)

```js
import mongoose from "mongoose";
await mongoose.connect(process.env.MONGO_URI);
const User = mongoose.model("User", { name: String });
const user = await User.create({ name: "Oleg" });
```

### PostgreSQL (pg)

```js
import { Client } from "pg";
const client = new Client({ connectionString: process.env.PG_URI });
await client.connect();
const res = await client.query("SELECT NOW()");
console.log(res.rows[0]);
```

### Prisma (ORM)

```js
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();
const newUser = await prisma.user.create({ data: { name: "Oleg" } });
```

---

## Авторизація, безпека, JWT, OAuth2, CSRF, Helmet

### JWT (jsonwebtoken)

```js
import jwt from "jsonwebtoken";
const token = jwt.sign({ userId: 1 }, process.env.JWT_SECRET, {
    expiresIn: "1h",
});
const payload = jwt.verify(token, process.env.JWT_SECRET);
```

### OAuth2 (passport.js)

```js
import passport from "passport";
// Додавай стратегию через passport-google-oauth20, passport-jwt, etc.
```

### CSRF (csurf)

```js
import csurf from "csurf";
app.use(csurf());
```

### Helmet (security headers)

```js
import helmet from "helmet";
app.use(helmet());
```

#### Best practices (безпека)

-   Зберігай секрети у `.env`.
-   Перевіряй всі дані з користувача (validation, sanitization).
-   HTTPS only для продакшену.
-   Використовуй security middleware (Helmet, csurf).
-   Регулярно оновлюй залежності, перевіряй через `npm audit`.

---

## Тестування (Jest, Vitest, Supertest, Mocha)

### Jest

```js
import { sum } from "./math";
test("сума чисел", () => {
    expect(sum(2, 3)).toBe(5);
});
```

### Supertest (HTTP API)

```js
import request from "supertest";
import app from "../src/app";

test("GET /", async () => {
    const res = await request(app).get("/");
    expect(res.statusCode).toBe(200);
});
```

### Vitest

```js
import { describe, it, expect } from "vitest";
describe("math", () => {
    it("сума", () => expect(sum(2, 2)).toBe(4));
});
```

### Mocha + Chai

```js
import { expect } from "chai";
describe("math", () => {
    it("сума", () => expect(sum(1, 2)).to.equal(3));
});
```

---

## TypeScript у Node.js

-   Додає типізацію та автокомпліт у серверний JS.
-   Використовуй `ts-node` для швидкого старту, або компілюй через `tsc`.

```json
// tsconfig.json (основні налаштування)
{
    "compilerOptions": {
        "target": "ES2022",
        "module": "NodeNext",
        "outDir": "./dist",
        "rootDir": "./src",
        "strict": true,
        "esModuleInterop": true
    }
}
```

### Приклад сервера на TypeScript

```ts
import express, { Request, Response } from "express";
const app = express();
app.get("/", (req: Request, res: Response) =>
    res.send("Hello TypeScript Node.js!")
);
app.listen(3000);
```

---

## Поглиблено: підкапотна робота Node.js (Event Loop, Streams, V8, GC, performance traps)

### Event Loop Deep Dive

-   Node.js Event Loop має фази: timers, pending callbacks, idle, poll, check, close callbacks.
-   Всі асинхронні операції (I/O, network, timers) ставляться у event queue, потім обробляються.
-   **libuv** — C-бібліотека, що забезпечує thread pool для асинхронних задач.

#### Візуалізація фаз event loop

```
┌───────────────┬────────────────┬───────────┬─────────┬─────────┬─────────────┐
│   timers      │ pending callbacks │ idle  │ poll    │ check   │ close cb    │
└───────────────┴────────────────┴───────────┴─────────┴─────────┴─────────────┘
```

### Streams Deep Dive

-   Streams (Readable, Writable, Duplex, Transform) — основа для роботи з великими даними, файлів, мережі.
-   Потоки асинхронні, ідеальні для обробки великих файлів, відео, аудіо, логів.

#### Приклад створення свого потоку

```js
import { Readable } from "stream";
const myStream = new Readable({
    read(size) {
        this.push("Hello stream!");
        this.push(null); // кінець потоку
    },
});
myStream.pipe(process.stdout);
```

### V8 та Garbage Collection

-   V8 оптимізує виконання JS через JIT.
-   GC (garbage collector) — очищає пам’ять, але може викликати паузи.
-   Важливо тримати короткі життєві цикли об’єктів, уникати глобальних reference.

### Performance traps

-   **Sync I/O:** викликає блокування event loop.
-   **Великі обчислення:** use worker_threads для багатопроцесорності.
-   **Memory leaks:** трекай використання пам’яті через `process.memoryUsage()`.
-   **Неправильне використання streams:** завжди оброблюй помилки потоку.

#### Performance profiling

```bash
node --inspect src/index.js
```

-   Використовуй інструменти: [Clinic.js](https://clinicjs.org/), [0x](https://github.com/davidmarkclements/0x), Chrome DevTools для профілювання Node.js.

---

## Типові підводні камені, security traps

-   **callback hell** — уникай вкладених колбеків, використовуй Promises/async/await.
-   **global variables** — не використовуй глобальні змінні для зберігання стану між запитами.
-   **неправильна робота з потоками** — завжди закривай потоки, обробляй помилки.
-   **неочищені дані користувача** — валідуй і санітайз дані.
-   **несвоєчасне оновлення залежностей** — регулярно перевіряй через `npm audit`.

---

## Best practices

-   Використовуй ESM, сучасний синтаксис.
-   Діли проект на модулі (MVC, routes, controllers, services).
-   Використовуй async/await для асинхронності.
-   Зберігай секрети у `.env`.
-   Валідуй всі вхідні дані.
-   Кешуй важкі запити (Redis, memcached).
-   Пиши юніт- та інтеграційні тести.
-   Використовуй TypeScript для типізації.
-   Регулярно оновлюй залежності, перевіряй через `npm audit`.
-   Документуй API через OpenAPI/Swagger.
-   Використовуй worker_threads/cluster для heavy tasks.
-   Профілюй продуктивність (Clinic.js, DevTools).
-   Впроваджуй security middleware (Helmet, csurf, rate-limit).

---

## Корисні ресурси та документація

-   [Node.js Docs](https://nodejs.org/en/docs/)
-   [Node.js Event Loop Guide](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)
-   [V8 Docs](https://v8.dev/)
-   [Express Docs](https://expressjs.com/)
-   [Fastify Docs](https://fastify.dev/)
-   [Hono Docs](https://hono.dev/)
-   [Mongoose Docs](https://mongoosejs.com/)
-   [Prisma Docs](https://www.prisma.io/docs/)
-   [Jest Docs](https://jestjs.io/)
-   [Vitest Docs](https://vitest.dev/)
-   [Supertest Docs](https://github.com/visionmedia/supertest)
-   [OpenAPI Docs](https://swagger.io/docs/)
-   [Clinic.js Performance Tools](https://clinicjs.org/)
-   [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
-   [Node.js Security Checklist](https://github.com/nodesecurity/nodesecurity)

---

## Короткий підсумок

**Node.js — це сучасна, асинхронна та продуктивна платформа для scalable backend, API, CLI та real-time-додатків.**  
Використовуй ESM, TypeScript, сучасні фреймворки (Express, Fastify, Hono), профілюй та тестуй код, дотримуйся best practices для безпеки, продуктивності та масштабування.  
Розбирайся у підкапотних механізмах (Event Loop, Streams, V8, GC, performance traps), щоб писати професійний і ефективний код!

---
