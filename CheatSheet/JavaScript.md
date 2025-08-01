# JavaScript Cheatsheet

## Basics
console.log('Hello')  
let x = 5  
const PI = 3.14  
var name = 'Ooodysseus'  
x += 1  
x++  
typeof x  
let y = x * 2  
let str = `Hello ${name}`  
let arr = [1,2,3]  
let obj = { a: 1, b: 2 }  
null, undefined, NaN  

## Data Types
Number  
String  
Boolean  
Object  
Array  
Function  
null  
undefined  
Symbol  

## Operators
+ - * / %  
++ --  
= += -= *= /=  
== != === !==  
> < >= <=  
&& || !  
? : (ternary)  

## String Methods
'abc'.length  
'abc'.toUpperCase()  
'abc'.toLowerCase()  
'abc'.replace('a','x')  
'abc'.includes('b')  
'abc'.split('')  
'abc'.indexOf('b')  
' abc '.trim()  
'abc'.charAt(1)  
'abc'.substring(1,2)  

## Number Methods
Math.round(2.5)  
Math.floor(2.9)  
Math.ceil(2.1)  
Math.max(1,2,3)  
Math.min(1,2,3)  
Math.random()  
parseInt('123')  
parseFloat('1.23')  
(1.23).toFixed(1)  

## Array Methods
arr.length  
arr.push(4)  
arr.pop()  
arr.shift()  
arr.unshift(0)  
arr.concat([5,6])  
arr.join(',')  
arr.slice(1,3)  
arr.splice(1,1)  
arr.indexOf(2)  
arr.includes(3)  
arr.map(x => x*2)  
arr.filter(x => x>1)  
arr.reduce((a,b)=>a+b,0)  
arr.forEach(x => console.log(x))  
arr.find(x => x>2)  
arr.sort()  
arr.reverse()  
[...arr] (spread)  

## Object Methods
Object.keys(obj)  
Object.values(obj)  
Object.entries(obj)  
Object.assign({}, obj)  
delete obj.a  
obj.hasOwnProperty('b')  
obj['a']  
obj.b  

## Functions
function sum(a,b) { return a+b }  
const sum = (a,b) => a+b  
function foo(...args) { return args }  
(function(){ ... })() // IIFE  
const double = x => x*2  
function greet(name='User') { return `Hello ${name}` }  

## Control Flow
if (x > 5) { ... }  
else if (x === 5) { ... }  
else { ... }  
switch(val) {  
  case 1: ...; break;  
  default: ...  
}  
for(let i=0; i<10; i++) { ... }  
for(const item of arr) { ... }  
for(const key in obj) { ... }  
while(x < 10) { x++ }  
do { ... } while(x < 5)  
break  
continue  
try { ... } catch(e) { ... } finally { ... }  
throw new Error('Fail')  

## Date & Time
new Date()  
Date.now()  
date.getFullYear()  
date.getMonth()  
date.getDate()  
date.getHours()  
date.getMinutes()  
date.toISOString()  
date.toLocaleString()  

## DOM Manipulation
document.getElementById('id')  
document.querySelector('.class')  
document.querySelectorAll('div')  
element.textContent = 'Hello'  
element.innerHTML = '<b>Bold</b>'  
element.classList.add('active')  
element.classList.remove('hide')  
element.setAttribute('data-id','123')  
element.getAttribute('href')  
element.style.color = 'red'  
document.createElement('div')  
parent.appendChild(child)  
parent.removeChild(child)  
element.addEventListener('click', fn)  
element.removeEventListener('click', fn)  

## Events
onclick  
onchange  
onsubmit  
oninput  
onmouseover  
onmouseout  
onkeydown  
onkeyup  
event.preventDefault()  
event.stopPropagation()  

## Timer
setTimeout(fn, 1000)  
setInterval(fn, 500)  
clearTimeout(timer)  
clearInterval(timer)  

## JSON
JSON.stringify(obj)  
JSON.parse(jsonStr)  

## Local Storage
localStorage.setItem('key','val')  
localStorage.getItem('key')  
localStorage.removeItem('key')  
localStorage.clear()  

## Session Storage
sessionStorage.setItem('key','val')  
sessionStorage.getItem('key')  

## Fetch & AJAX
fetch('/api/data')  
.then(res => res.json())  
.then(data => console.log(data))  
.catch(err => console.error(err))  

## Promises
const p = new Promise((res,rej)=>{ ... })  
p.then(val => ...).catch(err => ...).finally(() => ...)  
Promise.all([p1, p2])  
Promise.race([p1, p2])  
async function foo() { await bar() }  
await fetch(url)  

## Classes
class Animal {  
  constructor(name) { this.name = name }  
  speak() { console.log(this.name) }  
}  
class Dog extends Animal {  
  bark() { console.log('Woof') }  
}  
let d = new Dog('Rex')  
d.speak(); d.bark();  

## Modules
export const x = 5  
export function fn() {}  
export default x  
import { x, fn } from './file.js'  
import y from './file.js'  

## Destructuring
const [a, b] = arr  
const {x, y} = obj  
function foo({name, age}) { ... }  

## Spread & Rest
const arr2 = [...arr, 4]  
const obj2 = {...obj, c: 3}  
function sum(...nums) { return nums.reduce((a,b)=>a+b) }  

## Set & Map
const s = new Set([1,2,3])  
s.add(4); s.delete(2); s.has(1)  
const m = new Map()  
m.set('a',1); m.get('a'); m.delete('a')  

## Symbol
const sym = Symbol('desc')  
obj[sym] = 42  

## Error Handling
try { throw new Error('fail') }  
catch(e) { console.error(e.message) }  
finally { ... }  

## Regular Expressions
/abc/.test('abc')  
'text'.match(/t/)  
str.replace(/\d+/g, '-')  

## Math
Math.abs(-5)  
Math.pow(2,3)  
Math.sqrt(9)  
Math.random()  
Math.floor(Math.random()*10)  

## Window
window.location.href  
window.open(url)  
window.alert('Hello!')  
window.confirm('Are you sure?')  
window.prompt('Type:')  

## Navigator
navigator.userAgent  
navigator.geolocation.getCurrentPosition(fn)  

## History
history.back()  
history.forward()  
history.pushState({},'', '/new')  

## Document
document.title  
document.cookie  
document.body  

## Cookies
document.cookie = "name=Ooodysseus"  

## Miscellaneous
undefined  
NaN  
Infinity  
isNaN(x)  
isFinite(x)  
parseInt(str)  
parseFloat(str)  
Number(str)  
String(num)  
Boolean(val)  

## Useful Patterns
debounce  
throttle  
memoization  
callback  
observer  
singleton  

## Best Practices
Use let/const  
Avoid var  
Prefer === over ==  
Use arrow functions  
Keep functions pure  
Avoid global variables  
Use modules  
Validate user input  
Handle errors gracefully  
Use strict mode  
Use descriptive names  
Comment complex logic  
Optimize loops  
Keep code DRY  
Refactor old code  
Avoid deep nesting  
Minimize side effects  
Prefer immutability  
Test edge cases  
Use linters  
Document APIs  
Review dependencies  
Use promises/async  
Handle exceptions  
Use template literals  
Organize files  
Prefer for...of over for...in  
Minimize use of eval  
Use ES6+ features  
Version code  
Automate testing  
Monitor performance  
Profile bottlenecks  
Cache expensive results  
Limit DOM manipulation  
Use event delegation  
Optimize selectors  
Compress assets  
Support multiple browsers  
Test mobile  
Keep dependencies updated  
Prefer error-first callbacks  
Avoid callback hell  
Use try/catch for async  
Keep code modular  
Version releases  
Document changes  
Review security issues  
Avoid magic numbers  
Encapsulate logic  
Use type checks  
Handle null/undefined  
Avoid shadowing  
Minimize side effects  
Test in production  
Keep code readable  
Use constants  
Minimize global scope  
Support accessibility  
Version main files  
Comment intent  
Prefer named exports  
Automate builds  
Monitor usage  
Test user flows  
Backup important code  
Review code regularly  
Prefer arrow functions  
Test browser compatibility  
