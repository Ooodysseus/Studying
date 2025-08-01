# TypeScript: Від основ до advanced (повний конспект)

---

## Зміст

1. [Вступ: Що таке TypeScript, для чого він потрібен, переваги над JS](#вступ)
2. [Підключення TypeScript, компіляція, tsconfig, робота з tooling](#підключення)
3. [Синтаксис: типи, оголошення, базові правила](#синтаксис)
4. [Типи: примітиви, масиви, кортежі, enum, literal, union, intersection, any, unknown, never, void, null/undefined](#типи)
5. [Типи функцій: сигнатури, optional/required/overloads, default params, rest/spread](#типи-функцій)
6. [Об’єкти, типи об’єктів, індексні підписи, readonly, optional fields, Record, Partial, Pick, Omit](#об'єкти)
7. [Інтерфейси (interface), типи (type), різниця, розширення, implements](#інтерфейси)
8. [Класи, наслідування, public/private/protected, abstract, implements, статичні поля/методи, get/set, readonly](#класи)
9. [Generics: базові, обмеження (extends), default, generic functions, generic classes](#generics)
10. [Типізація масивів та об'єктів, mapped types, conditional types, infer](#типізація-масивів-об'єктів)
11. [Модулі, імпорт/експорт, namespace, declaration merging](#модулі)
12. [Декоратори, metadata, experimental features](#декоратори)
13. [Type Guards, type predicates, user-defined guards, assert](#type-guards)
14. [Типізація this, call/apply/bind, context, функції з дженериками](#типізація-this)
15. [Асинхронність, типізація промісів, async/await, типізація fetch/axios](#асинхронність)
16. [Типи для React/Vue/Node (JSX, Props, ReturnType, Context, типізація middleware, Express, etc)](#типи-для-фреймворків)
17. [Типові помилки, антипатерни, best practices, strict mode, tsconfig нюанси](#типові-помилки)
18. [Практичні поради, корисні утиліти, патерни, лінтери, сервіси](#практичні-поради)
19. [Корисні ресурси](#ресурси)

---

## 1. Вступ: Що таке TypeScript, для чого він потрібен, переваги над JS <a name="вступ"></a>

-   **TypeScript (TS)** — це надбудова над JavaScript, яка додає статичну типізацію, компіляцію, сучасний синтаксис, і покращену підтримку великих проектів.
-   Дозволяє знаходити помилки на етапі розробки, а не у рантаймі.
-   Підтримує всі JS-фічі + власні TS-фічі.

---

## 2. Підключення TypeScript, компіляція, tsconfig, робота з tooling <a name="підключення"></a>

-   **Встановлення:**  
    `npm install -g typescript`
-   **Компіляція:**  
    `tsc file.ts`  
    або `npx tsc`
-   **tsconfig.json** — основний конфіг для проекту.
    ```json
    {
        "compilerOptions": {
            "target": "es6",
            "module": "commonjs",
            "strict": true,
            "outDir": "./dist"
        },
        "include": ["src/**/*"],
        "exclude": ["node_modules"]
    }
    ```
-   **Інтеграція з build tools:** webpack, Vite, Babel, ts-node, Jest.

---

## 3. Синтаксис: типи, оголошення, базові правила <a name="синтаксис"></a>

```ts
let age: number = 25;
const name: string = "Ivan";
let isActive: boolean = true;
let user: { name: string; age: number };
let ids: number[] = [1, 2, 3];
let tuple: [string, number] = ["Alice", 23];

function sum(a: number, b: number): number {
    return a + b;
}
```

-   Типи пишуться після двокрапки.
-   Якщо тип не вказаний — TypeScript виводить тип сам (type inference).
-   Усі JS-файли — валідний TS (але не навпаки).

---

## 4. Типи: примітиви, масиви, кортежі, enum, literal, union, intersection, any, unknown, never, void, null/undefined <a name="типи"></a>

```ts
// Примітиви
let n: number;
let s: string;
let b: boolean;

// Масиви
let arr: string[] = ["a", "b"];
let arr2: Array<number> = [1, 2, 3];

// Кортежі (tuple)
let person: [string, number] = ["Tom", 30];

// Enum
enum Color {
    Red,
    Green,
    Blue,
}
let c: Color = Color.Green;

// Literal types
let dir: "up" | "down";

// Union / Intersection
let id: string | number;
type A = { a: number };
type B = { b: string };
type AB = A & B;

// any/unknown/never/void/null/undefined
let v: any;
let u: unknown;
function error(): never {
    throw new Error("X");
}
function log(msg: string): void {
    console.log(msg);
}
let nu: null = null;
let und: undefined = undefined;
```

---

## 5. Типи функцій: сигнатури, optional/required/overloads, default params, rest/spread <a name="типи-функцій"></a>

```ts
function greet(name: string, age?: number): string {
    return `Hello, ${name}`;
}
type GreetFn = (name: string, age?: number) => string;

function add(a: number, b: number = 1): number {
    return a + b;
} // default param

function sum(...nums: number[]): number {
    return nums.reduce((a, b) => a + b, 0);
}

// Overloads
function toStr(a: number): string;
function toStr(a: string): string;
function toStr(a: any): string {
    return String(a);
}
```

---

## 6. Об’єкти, типи об’єктів, індексні підписи, readonly, optional fields, Record, Partial, Pick, Omit <a name="об'єкти"></a>

```ts
type User = {
    id: number;
    name: string;
    email?: string; // optional
    readonly createdAt: Date;
};

let user: User = {
    id: 1,
    name: "Ivan",
    createdAt: new Date(),
};

// Індексні підписи:
type StringMap = { [key: string]: string };
let dict: StringMap = { uk: "Україна" };

// Utility types:
type UserPartial = Partial<User>;
type UserPick = Pick<User, "id" | "name">;
type UserOmit = Omit<User, "email">;
type UserRecord = Record<"id" | "name", string | number>;
```

---

## 7. Інтерфейси (interface), типи (type), різниця, розширення, implements <a name="інтерфейси"></a>

```ts
interface Person {
    name: string;
    age: number;
    greet(): void;
}
interface Employee extends Person {
    position: string;
}
type Admin = Person & { role: string };

class Developer implements Person {
    name: string;
    age: number;
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    greet() {
        console.log(`Hi, I'm ${this.name}`);
    }
}
```

-   **interface** — розширюється (extends), може бути merged.
-   **type** — не може бути merged, може бути union/intersection.

---

## 8. Класи, наслідування, public/private/protected, abstract, implements, статичні поля/методи, get/set, readonly <a name="класи"></a>

```ts
class Animal {
    public name: string;
    private age: number;
    protected type: string = "mammal";
    static counter = 0;
    readonly id: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
        this.id = ++Animal.counter;
    }
    get info() {
        return `${this.name} (${this.age})`;
    }
    set info(val: string) {
        this.name = val;
    }
}

abstract class Shape {
    abstract area(): number;
}
class Circle extends Shape {
    constructor(public r: number) {
        super();
    }
    area() {
        return Math.PI * this.r * this.r;
    }
}
```

---

## 9. Generics: базові, обмеження (extends), default, generic functions, generic classes <a name="generics"></a>

```ts
function identity<T>(arg: T): T {
    return arg;
}
const x = identity<string>("abc");

function merge<T extends object, U extends object>(a: T, b: U): T & U {
    return { ...a, ...b };
}

class Box<T = string> {
    value: T;
    constructor(val: T) {
        this.value = val;
    }
}
```

---

## 10. Типізація масивів та об'єктів, mapped types, conditional types, infer <a name="типізація-масивів-об'єктів"></a>

```ts
type User = { id: number; name: string };
type UserKeys = keyof User; // "id" | "name"

type ReadonlyUser = { readonly [K in keyof User]: User[K] };
type Nullable<T> = { [K in keyof T]: T[K] | null };

// Conditional types
type IsString<T> = T extends string ? true : false;
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;
```

---

## 11. Модулі, імпорт/експорт, namespace, declaration merging <a name="модулі"></a>

```ts
// user.ts
export type User = { id: number, name: string };
export function getUser(id: number): User { ... }

// main.ts
import { User, getUser } from './user';

// namespace
namespace MathLib {
  export function sum(a: number, b: number): number { return a + b; }
}
let s = MathLib.sum(1,2);

// Declaration merging:
interface Window { appLoaded: boolean; }
window.appLoaded = true;
```

---

## 12. Декоратори, metadata, experimental features <a name="декоратори"></a>

-   Декоратори працюють тільки з experimentalDecorators:true в tsconfig.

```ts
function Log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const orig = descriptor.value;
    descriptor.value = function (...args: any[]) {
        console.log("Call:", propertyKey, args);
        return orig.apply(this, args);
    };
}

class Test {
    @Log
    foo(x: number) {
        return x * 2;
    }
}
```

-   Декоратори застосовуються до класів, методів, властивостей, параметрів.

---

## 13. Type Guards, type predicates, user-defined guards, assert <a name="type-guards"></a>

```ts
function isString(x: unknown): x is string {
  return typeof x === "string";
}
function print(val: string | number) {
  if (isString(val)) { /* тут val: string */ }
  else { /* тут val: number */ }
}

// typeof, instanceof, in
if (typeof x === "number") { ... }
if (arr instanceof Array) { ... }
if ("name" in obj) { ... }
```

---

## 14. Типізація this, call/apply/bind, context, функції з дженериками <a name="типізація-this"></a>

```ts
function foo(this: HTMLDivElement, evt: MouseEvent) { ... }
const bound = foo.bind(divEl);

class Button {
  onClick(this: Button, evt: MouseEvent) { ... }
}
```

-   TS дозволяє явно типізувати this у функції.

---

## 15. Асинхронність, типізація промісів, async/await, типізація fetch/axios <a name="асинхронність"></a>

```ts
async function fetchUser(id: number): Promise<User> {
    const res = await fetch(`/api/user/${id}`);
    return res.json();
}

function delay(ms: number): Promise<void> {
    return new Promise((res) => setTimeout(res, ms));
}
```

-   Усі async-функції повертають `Promise<T>`.
-   Типізація fetch/axios: через дженерики або власні типи.

---

## 16. Типи для React/Vue/Node (JSX, Props, ReturnType, Context, типізація middleware, Express, etc) <a name="типи-для-фреймворків"></a>

**React:**

```tsx
type Props = { title: string; onClick?: () => void };
const Button: React.FC<Props> = ({ title, onClick }) => (
    <button onClick={onClick}>{title}</button>
);

// React Hooks: useState<number>(), useContext<MyContextType>()
// ReturnType, Parameters, InstanceType — утиліти для типів функцій
```

**Node/Express:**

```ts
import { Request, Response, NextFunction } from "express";
const mw: (req: Request, res: Response, next: NextFunction) => void = (req, res, next) => { ... }
```

**Vue:**

-   Власні типи для пропсів, компонентів, event-об'єктів.

---

## 17. Типові помилки, антипатерни, best practices, strict mode, tsconfig нюанси <a name="типові-помилки"></a>

-   Не використовувати any без нагальної потреби.
-   Не використовувати //@ts-ignore без пояснення.
-   Типи мусять відповідати реальним даним.
-   Дублювання типів (DRY через utility types).
-   Не завжди потрібен interface — часто type зручніше.
-   Використовуй strict:true у tsconfig, перевіряй noImplicitAny, noUnusedLocals.

---

## 18. Практичні поради, корисні утиліти, патерни, лінтери, сервіси <a name="практичні-поради"></a>

-   Використовуй типи для документації API.
-   Пиши типи для всього “на вході” і “на виході” функцій.
-   Зберігай типи DRY, не дублюй.
-   Використовуй eslint + typescript-eslint для перевірки.
-   Перевіряй проект через `tsc --noEmit` для чистоти типів.
-   Utility types: Partial, Required, Pick, Omit, Record, ReturnType, InstanceType, NonNullable, Exclude, Extract.
-   Для великих проектів — розбивай на власні .d.ts файли.

---

## 19. Корисні ресурси <a name="ресурси"></a>

-   [Офіційно: typescriptlang.org](https://www.typescriptlang.org/)
-   [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
-   [TS Deep Dive (Basarat)](https://basarat.gitbook.io/typescript/)
-   [Type Challenges (вправи)](https://github.com/type-challenges/type-challenges)
-   [DefinitelyTyped (типи для всіх популярних бібліотек)](https://github.com/DefinitelyTyped/DefinitelyTyped)
-   [TypeScript playground](https://www.typescriptlang.org/play)

---

**TypeScript — це сучасний стандарт для розробки підтримуваних, масштабованих і безпечних фронтенд/бекенд проектів. Глибоке розуміння TS = мінімум багів, максимум швидкості у розробці!**
