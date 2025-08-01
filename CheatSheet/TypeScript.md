# TypeScript Cheatsheet

## Basics
let x: number = 5  
let name: string = "Ooodysseus"  
let active: boolean = true  
let arr: number[] = [1, 2, 3]  
let data: Array<string> = ['a', 'b']  
let obj: { a: number, b: string } = { a: 1, b: 'x' }  
let value: any = 42  
let unk: unknown = 'test'  
let nullable: string | null = null  

## Type Inference
let y = 10        // inferred as number  
let z = 'abc'     // inferred as string  

## Union & Intersection
let id: number | string = 123  
type A = { a: number }  
type B = { b: string }  
type C = A & B      // { a: number, b: string }  

## Literal Types
let dir: 'up' | 'down' = 'up'  

## Enums
enum Color { Red, Green, Blue }  
let c: Color = Color.Green  
enum Status { Active = 1, Inactive = 0 }  

## Tuples
let pair: [number, string] = [1, 'a']  

## Functions
function add(a: number, b: number): number { return a + b }  
const mul = (x: number, y: number): number => x * y  
function log(msg: string, ...args: any[]): void { console.log(msg, ...args) }  
function greet(name?: string): string { return `Hello ${name ?? 'User'}` }  

## Return Types
function getData(): string | undefined { return undefined }  
function neverError(): never { throw new Error('fail') }  

## Type Aliases
type User = { id: number; name: string; }  
type Point = [number, number]  

## Interfaces
interface IUser { id: number; name: string; }  
interface Animal { speak(): void }  
interface Dog extends Animal { bark(): void }  
let u: IUser = { id: 1, name: 'Ooodysseus' }  

## Optional Properties
type Car = { model: string; year?: number }  
let car: Car = { model: 'Tesla' }  

## Readonly
interface Config { readonly apiKey: string }  

## Index Signatures
interface Dict { [key: string]: number }  
let scores: Dict = { 'a': 10, 'b': 15 }  

## Type Assertions
let val: any = "42"  
let num = (val as number)  
let str = <string>val  

## Generics
function wrap<T>(value: T): T[] { return [value] }  
class Box<T> { constructor(public value: T) {} }  
interface ApiResponse<T> { data: T; error?: string }  

## keyof & typeof
type Keys = keyof User        // "id" | "name"  
const user = { id: 1, name: 'Ooodysseus' }  
type UserType = typeof user   // { id: number, name: string }  

## Mapped Types
type ReadonlyUser = { readonly [K in keyof User]: User[K] }  

## Conditional Types
type IsString<T> = T extends string ? true : false  
type Result = IsString<number> // false  

## Utility Types
Partial<User>  
Required<User>  
Readonly<User>  
Pick<User, 'id'>  
Omit<User, 'name'>  
Record<string, number>  
ReturnType<typeof add>  
Parameters<typeof log>  
NonNullable<string | null>  
Exclude<'a' | 'b', 'a'>  
Extract<'a' | 'b', 'c', 'b' | 'c'>  

## Classes
class Animal {  
  name: string  
  constructor(name: string) { this.name = name }  
  speak(): void { console.log(this.name) }  
}  
class Dog extends Animal {  
  bark(): void { console.log('Woof!') }  
}  
const d = new Dog('Rex')  
d.speak(); d.bark();  

## Access Modifiers
class User {  
  public name: string  
  private password: string  
  protected role: string  
  constructor(name: string, password: string, role: string) {  
    this.name = name  
    this.password = password  
    this.role = role  
  }  
}  

## Static Properties
class Counter {  
  static count = 0  
  static inc() { this.count++ }  
}  
Counter.inc()  

## Abstract Classes
abstract class Shape {  
  abstract area(): number  
}  
class Circle extends Shape {  
  constructor(public r: number) { super() }  
  area() { return Math.PI * this.r * this.r }  
}  

## Implements
interface Logger { log(msg: string): void }  
class ConsoleLogger implements Logger { log(msg: string) { console.log(msg) } }  

## Namespaces
namespace Utils {  
  export function sum(a: number, b: number) { return a + b }  
}  
Utils.sum(1,2)  

## Modules
export function fn() {}  
export const x = 5  
export default fn  
import { fn, x } from './file'  
import y from './file'  

## Decorators
function Log(target: any, key: string) { /* ... */ }  
class Test {  
  @Log  
  method() {}  
}  

## Async/Await
async function fetchData(): Promise<string> {  
  return await Promise.resolve('data')  
}  
await fetchData()  

## Error Handling
try { throw new Error('fail') }  
catch (e) { console.error(e) }  
finally { /* ... */ }  

## DOM Types
let el: HTMLElement | null = document.getElementById('myId')  
el?.classList.add('active')  

## Type Guards
function isString(x: any): x is string { return typeof x === 'string' }  
if (isString(val)) { val.toUpperCase() }  

## Discriminated Unions
type Shape =  
  | { kind: 'circle'; r: number }  
  | { kind: 'square'; size: number }  
function area(s: Shape) {  
  switch (s.kind) {  
    case 'circle': return Math.PI * s.r * s.r  
    case 'square': return s.size * s.size  
  }  
}  

## Nullish Coalescing
let a = val ?? 'default'  

## Optional Chaining
let size = obj?.prop?.subProp  

## tsconfig.json
{  
  "compilerOptions": {  
    "target": "ESNext",  
    "module": "ESNext",  
    "strict": true,  
    "esModuleInterop": true,  
    "outDir": "dist",  
    "sourceMap": true  
  }  
}  

## Type Checking
tsc  
tsc --noEmit  
tsc --watch  

## Linting
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev  
npx eslint .  

## Type Declaration Files
declare module 'my-lib'  
declare function foo(a: number): string  

## JSDoc
/**  
 * Adds two numbers  
 * @param a  
 * @param b  
 * @returns number  
 */  
function sum(a: number, b: number): number { return a + b }  

## Best Practices
Enable strict mode  
Keep types simple  
Use interfaces for objects  
Prefer type aliases for unions  
Document functions  
Use readonly where possible  
Limit any/unknown usage  
Validate user input  
Keep code DRY  
Comment complex logic  
Write tests  
Use automated type checking  
Keep tsconfig clean  
Prefer const/let  
Avoid var  
Refactor old code  
Organize files  
Minimize global scope  
Use modules  
Prefer ES6+ features  
Automate builds  
Lint code  
Update dependencies  
Version releases  
Use error boundaries  
Test edge cases  
Backup configs  
Monitor logs  
Optimize imports  
Prefer functional code  
Review security updates  
Document types  
Support multiple platforms  
Handle null/undefined  
Prefer discriminated unions  
Use generics for reuse  
Avoid magic numbers  
Keep changelog  
Optimize for performance  
Support containers  
Automate deployment  
Test real-world flows  
Comment intent  
Keep code readable  
Document API  
Version schemas  
Keep structure logical  
Review updates  
Limit ambient declarations  
Test user flows  
Archive unused code  
Keep README updated  
