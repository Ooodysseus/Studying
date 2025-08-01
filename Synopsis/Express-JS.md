# Express.js (Express): сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке Express.js](#що-таке-expressjs)
-   [Роль Express.js у сучасному Node.js стеку](#роль-expressjs-у-сучасному-nodejs-стеку)
-   [Встановлення та старт проекту](#встановлення-та-старт-проекту)
-   [Структура проекту, архітектура](#структура-проекту-архітектура)
-   [Створення серверу та основні концепції](#створення-серверу-та-основні-концепції)
-   [Роутінг (Routing), параметри, query, body](#роутінг-routing-параметри-query-body)
-   [Middleware: принцип роботи, типи, advanced](#middleware-принцип-роботи-типи-advanced)
-   [Обробка помилок (Error Handling)](#обробка-помилок-error-handling)
-   [Взаємодія з базами даних (MongoDB, PostgreSQL, Prisma, Mongoose)](#взаємодія-з-базами-даних-mongodb-postgresql-prisma-mongoose)
-   [Внутрішні механізми: event loop, middleware pipeline, performance traps](#внутрішні-механізми-event-loop-middleware-pipeline-performance-traps)
-   [Поглиблено: Express internals, req/res, closure, async traps, memory, streams](#поглиблено-express-internals-reqres-closure-async-traps-memory-streams)
-   [Безпека: Helmet, CORS, CSRF, rate limiting, validation](#безпека-helmet-cors-csrf-rate-limiting-validation)
-   [Авторизація та автентифікація (JWT, OAuth2, Passport.js)](#авторизація-та-автентифікація-jwt-oauth2-passportjs)
-   [Тестування (Jest, Supertest, Vitest, Mocha)](#тестування-jest-supertest-vitest-mocha)
-   [TypeScript у Express.js](#typescript-у-expressjs)
-   [Best practices](#best-practices)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**Express.js (Express)** — це найпопулярніший фреймворк для Node.js, який дозволяє швидко та гнучко будувати HTTP сервери, REST API, мікросервіси, GraphQL, SSR, реальний час (real-time) та серверну логіку для сучасних web-додатків.  
Express створює базу для scalable, maintainable та безпечних серверних рішень.

---

## Що таке Express.js

-   **Express.js** — це мінімалістичний, гнучкий фреймворк для створення web-серверів та API на Node.js.
-   Має модульну систему middleware, простий роутінг, велику екосистему плагінів.
-   Підтримує ESM та TypeScript, інтеграцію з будь-якими базами даних і сторонніми бібліотеками.

---

## Роль Express.js у сучасному Node.js стеку

-   Базовий фреймворк для REST API, GraphQL, SSR, WebSocket.
-   Інтегрується з такими технологіями, як MongoDB, PostgreSQL, Redis, Prisma, Mongoose.
-   Використовується у JAMstack, serverless, microservices, cloud native.
-   Підходить для малих стартапів і великих enterprise додатків.

---

## Встановлення та старт проекту

### Встановлення Express через npm

```bash
npm install express
```

### Створення базового серверу

```js
import express from "express";
const app = express();

app.get("/", (req, res) => res.send("Hello Express!"));

app.listen(3000, () => {
    console.log("Server started on http://localhost:3000");
});
```

### Старт проекту зі структурою

```
express-app/
├─ src/
│  ├─ app.js
│  ├─ routes/
│  ├─ controllers/
│  ├─ middlewares/
│  ├─ models/
│  └─ utils/
├─ tests/
├─ package.json
├─ .env
├─ .gitignore
```

---

## Структура проекту, архітектура

-   **routes/** — маршрутизація, групування endpoint-ів.
-   **controllers/** — бізнес-логіка, обробка запитів/відповідей.
-   **middlewares/** — функції-посередники для обробки запитів (логування, автентифікація, body parsing).
-   **models/** — схеми для бази даних.
-   **utils/** — утиліти, хелпери, сервіси.
-   **tests/** — юніт- та інтеграційні тести.

---

## Створення серверу та основні концепції

### Базовий сервер

```js
import express from "express";
const app = express();

app.use(express.json()); // парсинг JSON body
app.get("/", (req, res) => res.send("Hello!"));
app.listen(3000);
```

### Обробка запитів

```js
app.get("/user/:id", (req, res) => {
    const { id } = req.params;
    res.json({ id });
});

app.post("/data", (req, res) => {
    const { name, email } = req.body;
    res.json({ name, email });
});
```

---

## Роутінг (Routing), параметри, query, body

-   **Маршрути** — групуй через окремі файли.
-   **Параметри** — через `:param` у шляху.
-   **Query** — через `req.query`.
-   **Body** — через `req.body` (парсинг через middleware).

### Приклад роутера

```js
import { Router } from "express";
const router = Router();

router.get("/users/:id", (req, res) => {
    res.json({ id: req.params.id });
});

router.get("/search", (req, res) => {
    res.json({ q: req.query.q });
});

router.post("/users", (req, res) => {
    res.json(req.body);
});

export default router;
```

### Підключення роутера

```js
import userRoutes from "./routes/users.js";
app.use("/api", userRoutes);
```

---

## Middleware: принцип роботи, типи, advanced

-   **Middleware** — функції, що мають доступ до req, res, next.
-   Використовуються для логування, валідації, авторизації, парсингу, обробки помилок.

### Приклад middleware

```js
const logger = (req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
};
app.use(logger);
```

### Advanced middleware (async)

```js
const asyncMiddleware = (fn) => (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
};
app.get(
    "/data",
    asyncMiddleware(async (req, res) => {
        const data = await getData();
        res.json(data);
    })
);
```

---

## Обробка помилок (Error Handling)

### Стандартний error handler

```js
app.use((err, req, res, next) => {
    console.error("Error:", err.message);
    res.status(500).json({ error: err.message });
});
```

-   Використовуй `next(err)` для передачі помилки.
-   Для async middleware — обов’язково обробляй `catch`.

---

## Взаємодія з базами даних (MongoDB, PostgreSQL, Prisma, Mongoose)

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
const result = await client.query("SELECT NOW()");
console.log(result.rows[0]);
```

### Prisma (ORM)

```js
import { PrismaClient } from "@prisma/client";
const prisma = new PrismaClient();
const user = await prisma.user.create({ data: { name: "Oleg" } });
```

---

## Внутрішні механізми: event loop, middleware pipeline, performance traps

-   **Event Loop** — неблокуюча архітектура (див. Node.js конспект).
-   **Middleware pipeline** — послідовність викликів, де кожен middleware може змінити request, response, викликати next().
-   **Performance traps:** блокуючий код, sync I/O, великі JSON, неочищені дані.

#### Схема middleware pipeline

```
Request → [mw1] → [mw2] → [route handler] → [error handler] → Response
```

---

## Поглиблено: Express internals, req/res, closure, async traps, memory, streams

### Як працює req/res

-   **req (Request):** інкапсулює HTTP-запит, має params, body, query, headers, cookies.
-   **res (Response):** методи для відповіді (res.send, res.json, res.status, res.end).

### Closure в middleware

-   Можна створювати параметризовані middleware через замикання.

```js
const auth = (role) => (req, res, next) => {
    if (req.user.role !== role)
        return res.status(403).json({ error: "forbidden" });
    next();
};
app.use(auth("admin"));
```

### Async traps

-   Не забувай обробляти помилки в async middleware.
-   Використовуй centralized error handling.

### Memory & Streams

-   Express підтримує роботу з потоками: можна стрімити файли, відео, дані.
-   Для великих відповідей — використовуй streams замість буферизації.

```js
app.get("/video", (req, res) => {
    const stream = fs.createReadStream("./video.mp4");
    stream.pipe(res);
});
```

---

## Безпека: Helmet, CORS, CSRF, rate limiting, validation

### Helmet

```js
import helmet from "helmet";
app.use(helmet());
```

### CORS

```js
import cors from "cors";
app.use(cors({ origin: "https://your-frontend.com" }));
```

### CSRF

```js
import csurf from "csurf";
app.use(csurf());
```

### Rate limiting

```js
import rateLimit from "express-rate-limit";
app.use(rateLimit({ windowMs: 60000, max: 100 }));
```

### Validation

-   Використовуй joi, zod, express-validator.

```js
import { body, validationResult } from "express-validator";
app.post(
    "/users",
    [body("email").isEmail(), body("password").isLength({ min: 8 })],
    (req, res) => {
        const errors = validationResult(req);
        if (!errors.isEmpty())
            return res.status(400).json({ errors: errors.array() });
        // Далі логіка
    }
);
```

---

## Авторизація та автентифікація (JWT, OAuth2, Passport.js)

### JWT

```js
import jwt from "jsonwebtoken";
const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET, {
    expiresIn: "1h",
});
const payload = jwt.verify(token, process.env.JWT_SECRET);
```

### OAuth2 (Passport.js)

```js
import passport from "passport";
import { Strategy as GoogleStrategy } from "passport-google-oauth20";
passport.use(
    new GoogleStrategy(
        {
            clientID: process.env.GOOGLE_ID,
            clientSecret: process.env.GOOGLE_SECRET,
            callbackURL: "/auth/google/callback",
        },
        (accessToken, refreshToken, profile, done) => {
            // знайти або створити юзера
            done(null, profile);
        }
    )
);
```

### Middleware для захисту роутів

```js
const authMiddleware = (req, res, next) => {
    const token = req.headers.authorization?.split(" ")[1];
    if (!token) return res.status(401).json({ error: "not authorized" });
    try {
        req.user = jwt.verify(token, process.env.JWT_SECRET);
        next();
    } catch (e) {
        res.status(401).json({ error: "invalid token" });
    }
};
```

---

## Тестування (Jest, Supertest, Vitest, Mocha)

### Jest

```js
import { sum } from "./math";
test("сума", () => {
    expect(sum(2, 3)).toBe(5);
});
```

### Supertest

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

## TypeScript у Express.js

-   Додає типізацію для request, response, middleware.
-   Використовуй @types/express для автокомпліту.

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

### Basic TypeScript Express server

```ts
import express, { Request, Response, NextFunction } from "express";
const app = express();

app.get("/", (req: Request, res: Response) => res.send("Hello TypeScript!"));

app.use((err: Error, req: Request, res: Response, next: NextFunction) => {
    res.status(500).json({ error: err.message });
});

app.listen(3000);
```

---

## Best practices

-   Діли проект на роутери, контролери, middleware.
-   Використовуй async/await, обробляй всі помилки.
-   Валідуй всі дані з клієнта (express-validator, joi, zod).
-   Використовуй centralized error handler.
-   Додавай security middleware (Helmet, CORS, rate-limit, csurf).
-   Використовуй environment-змінні для секретів.
-   Пиши юніт- та інтеграційні тести (Jest/Supertest).
-   Документуй API (Swagger/OpenAPI).
-   Не зберігай стан у глобальних змінних.
-   Стрім дані для великих відповідей (файли, відео).
-   Оновлюй залежності, перевіряй через `npm audit`.

---

## Корисні ресурси та документація

-   [Express Docs](https://expressjs.com/)
-   [Express API Reference](https://expressjs.com/en/4x/api.html)
-   [Node.js Docs](https://nodejs.org/en/docs/)
-   [Mongoose Docs](https://mongoosejs.com/)
-   [Prisma Docs](https://www.prisma.io/docs/)
-   [Passport.js Docs](http://www.passportjs.org/docs/)
-   [Jest Docs](https://jestjs.io/)
-   [Supertest Docs](https://github.com/visionmedia/supertest)
-   [Vitest Docs](https://vitest.dev/)
-   [Swagger Docs](https://swagger.io/docs/)
-   [Express Best Practices](https://github.com/expressjs/expressjs.com#best-practices)
-   [Node.js Security Checklist](https://github.com/nodesecurity/nodesecurity)

---

## Короткий підсумок

**Express.js — сучасний, гнучкий фреймворк для Node.js, що дозволяє швидко створювати REST API, SSR, real-time додатки, мікросервіси.**  
Дотримуйся модульної структури, використовуй middleware, TypeScript, сучасні підходи до безпеки, валідації та тестування.  
Описуй API у Swagger, профілюй продуктивність, стеж за безпекою та оновленням залежностей.  
Розбирайся у підкапотних механізмах Express і Node.js — це основа для професійної розробки у 2024+!

---
