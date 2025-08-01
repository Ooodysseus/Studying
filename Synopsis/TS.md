# Ultimate TypeScript Cheat Sheet

## ⭐ Description

TypeScript (TS) is a typed superset of JavaScript that compiles to plain JS. It adds static typing, interfaces, generics, enums, and tooling for large-scale projects.

## ⭐ Relationship With Other Technologies

-   JS: TS is JS with types—all JS is valid TS.
-   Vue/Angular/Nuxt/Electron: TS is used for logic and type safety.
-   Node/Express: TS can be used for server-side code.
-   Electron: TS used for desktop app logic.

---

## 1. Basic Types

```ts
let num: number = 10;
let str: string = "Hello";
let isDone: boolean = false;
let arr: number[] = [1, 2, 3];
let tuple: [string, number] = ["age", 30];
let anyVar: any = "anything";
let unknownVar: unknown = 123;
let nullable: number | null = null;
let union: string | number = "hi";
let literal: "ON" | "OFF" = "ON";
```

---

## 2. Enums

```ts
enum Direction {
    Up,
    Down,
    Left,
    Right,
}
let dir: Direction = Direction.Up;
enum Status {
    Success = 200,
    Error = 500,
}
```

---

## 3. Interfaces & Types

```ts
interface User {
    id: number;
    name: string;
    email?: string; // Optional
}
const user: User = { id: 1, name: "John" };

type Point = { x: number; y: number };
let pt: Point = { x: 0, y: 0 };

type StringOrNum = string | number;
```

---

## 4. Functions

```ts
function add(a: number, b: number): number {
    return a + b;
}
const sub = (a: number, b: number): number => a - b;
function log(msg: string, level: "info" | "warn" | "error" = "info"): void {}
```

---

## 5. Classes & OOP

```ts
class Animal {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    speak(): void {
        console.log(`${this.name} speaks.`);
    }
}
class Dog extends Animal {
    speak(): void {
        console.log(`${this.name} barks.`);
    }
}
```

---

## 6. Generics

```ts
function identity<T>(value: T): T {
    return value;
}
let out = identity<number>(10);

interface ApiResponse<T> {
    data: T;
    error?: string;
}
```

---

## 7. Type Assertions

```ts
let x: any = "hello";
let len = (x as string).length;
let len2 = (<string>x).length;
```

---

## 8. Advanced Types

-   `Partial<T>`: All props optional
-   `Readonly<T>`: All props readonly
-   `Record<K, T>`: Map keys to type
-   `Pick<T, K>`: Subset of props
-   `Omit<T, K>`: All except K

```ts
type UserPartial = Partial<User>;
type UserReadonly = Readonly<User>;
type IdMap = Record<string, number>;
type NameOnly = Pick<User, "name">;
type NoEmail = Omit<User, "email">;
```

---

## 9. Modules

```ts
// Export
export function foo() { ... }
export default class Bar { ... }

// Import
import { foo } from './foo';
import Bar from './bar';
```

---

## 10. Decorators (Angular)

```ts
@Component({ selector: "app-root", templateUrl: "./app.component.html" })
export class AppComponent {}
```

---

## 11. Utility Types

```ts
type Optional<T> = { [K in keyof T]?: T[K] };
type Required<T> = { [K in keyof T]-?: T[K] };
type Mapped<T> = { [K in keyof T]: T[K] };
```

---

## 12. Type Guards

```ts
function isString(x: any): x is string {
    return typeof x === "string";
}
```

---

## 13. Error Handling

```ts
try { ... } catch (e) { ... }
```

---

## 14. Configuration (`tsconfig.json`)

```json
{
    "compilerOptions": {
        "target": "ES2020",
        "module": "commonjs",
        "strict": true,
        "esModuleInterop": true,
        "outDir": "./dist",
        "sourceMap": true,
        "types": ["node", "jest"]
    }
}
```

---

## 15. ESLint/TSLint

-   Use [ESLint](https://eslint.org/) with typescript plugin.
-   Run `npx eslint . --ext .ts,.tsx`
-   Use [Prettier](https://prettier.io/) for code formatting.

---

## 16. Best Practices

-   Use explicit types.
-   Prefer interfaces for object shapes.
-   Avoid `any`; prefer `unknown` for safety.
-   Use strict mode.
-   Use type inference where possible.
-   Keep types modular, DRY, and reusable.
-   Use generics for reusable components.

---

## 17. Tools & Resources

-   [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
-   [DefinitelyTyped](https://definitelytyped.org/)
-   [tsconfig Reference](https://www.typescriptlang.org/tsconfig)
-   [TS Playground](https://www.typescriptlang.org/play)

---

## 18. Interoperability Table

| Feature       | TS  | JS  | HTML | CSS/SCSS | Vue/Angular/Nuxt | Node/Express | Electron |
| ------------- | --- | --- | ---- | -------- | ---------------- | ------------ | -------- |
| Static Types  | ✔️  |     |      |          | ✔️               | ✔️           | ✔️       |
| Module System | ✔️  | ✔️  |      |          | ✔️               | ✔️           | ✔️       |
| Decorators    | ✔️  |     |      |          | ✔️ (Angular)     |              |          |
