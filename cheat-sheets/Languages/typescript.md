# TYPESCRIPT

TypeScript — мова програмування, надмножина JavaScript з підтримкою статичної типізації, інтерфейсів, класів, generics і сучасних можливостей для розробки масштабованих додатків.

## Категорія: Типи та оголошення

| Команда/метод          | Опис        | Приклад/Аутпут                   |
| ---------------------- | ----------- | -------------------------------- | ---------------------------- |
| let x: number          | число       | let x: number = 5                |
| const s: string        | рядок       | const s: string = 'hi'           |
| let arr: number[]      | масив чисел | let arr: number[] = [1,2,3]      |
| let t: [string,number] | кортеж      | let t: [string,number] = ['a',1] |
| type User = {...}      | власний тип | type User = {id:number}          |
| interface IUser {...}  | інтерфейс   | interface IUser {id:number}      |
| enum Role {...}        | перелік     | enum Role {Admin,User}           |
| any/unknown/never/void | спец. типи  | let x: any; let y: unknown; ...  |
| let u: undefined       | null        | спец. значення                   | let u: undefined = undefined |
| let f: Function        | тип функції | let f: (a:number)=>void          |
| let obj: object        | об'єкт      | let obj: object = {a:1}          |

## Категорія: Робота з масивами та об'єктами

| Команда/метод    | Опис                 | Приклад/Аутпут                   |
| ---------------- | -------------------- | -------------------------------- |
| Array<number>    | generic-масив        | let arr: Array<number> = [1,2,3] |
| ReadonlyArray<T> | тільки для читання   | let arr: ReadonlyArray<number>   |
| Record<K,V>      | об'єкт-словник       | Record<string,number>            |
| Partial<T>       | часткова типізація   | Partial<User>                    |
| Required<T>      | всі поля обов'язкові | Required<User>                   |
| Pick<T,K>        | вибір полів          | Pick<User, 'id'>                 |
| Omit<T,K>        | виключення полів     | Omit<User, 'id'>                 |
| keyof T          | ключі типу           | type K = keyof User              |
| typeof obj       | тип за значенням     | type T = typeof obj              |

## Категорія: Функції та generics

| Команда/метод                | Опис                 | Приклад/Аутпут                        |
| ---------------------------- | -------------------- | ------------------------------------- | -------------------- | --------- |
| function fn(a:number):string | типізація аргументів | function sum(a:number):string{}       |
| const f = <T>(x:T):T=>x      | generic-функція      | const id = <T>(x:T)=>x                |
| (a: string                   | number)              | union-тип                             | function f(a: string | number){} |
| (a?: number)                 | необов'язковий       | function f(a?:number){}               |
| (a: number = 1)              | значення за замовч.  | function f(a: number = 1){}           |
| (...args: any[])             | решта аргументів     | function f(...args:any[]){}           |
| overloads                    | перевантаження       | function f(a:string):void; f(1):void; |

## Категорія: Класи та модифікатори

| Команда/метод            | Опис                    | Приклад/Аутпут                          |
| ------------------------ | ----------------------- | --------------------------------------- |
| class User { ... }       | клас                    | class User {id:number;}                 |
| implements/extends       | реалізація/наслідування | class A implements I; class B extends A |
| public/private/protected | модифікатори доступу    | private id:number                       |
| readonly                 | тільки для читання      | readonly name:string                    |
| static                   | статичне поле/метод     | static count:number                     |
| constructor              | конструктор             | constructor(id:number)                  |
| super()                  | виклик батьківського    | super()                                 |

## Категорія: Advanced Types

| Команда/метод           | Опис               | Приклад/Аутпут                  |
| ----------------------- | ------------------ | ------------------------------- | -------------- | --- |
| type A = B & C          | intersection       | type AB = A & B                 |
| type A = B              | C                  | union                           | type AB = A    | B   |
| type X = Exclude<A,B>   | виключити типи     | Exclude<'a'                     | 'b','a'> → 'b' |
| type X = Extract<A,B>   | залишити типи      | Extract<'a'                     | 'b','a'> → 'a' |
| type X = NonNullable<T> | без null/undefined | NonNullable<string              | null> → string |
| infer                   | виведення типу     | type R = ReturnType<()=>number> |

## Категорія: Type Guards та Assertions

| Команда/метод         | Опис                | Приклад/Аутпут                    |
| --------------------- | ------------------- | --------------------------------- |
| typeof x === 'string' | перевірка типу      | if(typeof x==='string'){}         |
| x instanceof C        | екземпляр класу     | if(x instanceof User){}           |
| as Type               | assertion           | x as number                       |
| <Type>x               | assertion (JSX off) | <number>x                         |
| is Type               | type guard          | function isStr(x:any):x is string |

## Категорія: Модулі та імпорт/експорт

| Команда/метод                | Опис              | Приклад/Аутпут                         |
| ---------------------------- | ----------------- | -------------------------------------- |
| export/import                | експорт/імпорт    | export const x=1; import {x} from './' |
| export default               | дефолтний експорт | export default function(){}            |
| import \* as name from 'mod' | імпорт всього     | import \* as fs from 'fs'              |

## Категорія: Utility Types

| Команда/метод  | Опис                 | Приклад/Аутпут                  |
| -------------- | -------------------- | ------------------------------- | -------------- |
| Readonly<T>    | тільки для читання   | Readonly<User>                  |
| Partial<T>     | часткова типізація   | Partial<User>                   |
| Required<T>    | всі поля обов'язкові | Required<User>                  |
| Pick<T,K>      | вибір полів          | Pick<User, 'id'>                |
| Omit<T,K>      | виключення полів     | Omit<User, 'id'>                |
| Record<K,T>    | словник              | Record<string,number>           |
| Exclude<T,U>   | виключити типи       | Exclude<'a'                     | 'b','a'> → 'b' |
| Extract<T,U>   | залишити типи        | Extract<'a'                     | 'b','a'> → 'a' |
| NonNullable<T> | без null/undefined   | NonNullable<string              | null> → string |
| ReturnType<F>  | тип повернення       | ReturnType<()=>number> → number |
| Parameters<F>  | тип аргументів       | Parameters<(a:number)=>void>    |

## Категорія: Інше

| Команда/метод      | Опис                 | Приклад/Аутпут                        |
| ------------------ | -------------------- | ------------------------------------- |
| // @ts-ignore      | ігнорувати помилку   | // @ts-ignore                         |
| declare var x      | оголошення глобально | declare var $:any                     |
| namespace N { }    | простір імен         | namespace Math {export const pi=3.14} |
| typeof import('m') | тип модуля           | type T = typeof import('fs')          |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
