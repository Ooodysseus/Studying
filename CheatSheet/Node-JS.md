# Node JS Cheatsheet

## Install & Init
npm install -g node  
node -v  
npm init -y  
npm install express  
npm install nodemon --save-dev  
node app.js  
nodemon app.js  

## Basic Script
console.log('Hello Node')  
process.exit(0)  

## Global Objects
process  
__dirname  
__filename  
global  

## Modules
require('module')  
const fs = require('fs')  
const path = require('path')  
const os = require('os')  
const http = require('http')  
const url = require('url')  
const crypto = require('crypto')  
const util = require('util')  
const events = require('events')  
const child_process = require('child_process')  

## Export/Import
module.exports = fn  
exports.fn = fn  
const fn = require('./fn')  

## File System
fs.readFile('file.txt', 'utf8', (err, data) => { ... })  
fs.writeFile('file.txt', 'text', () => {})  
fs.appendFile('file.txt', 'more', () => {})  
fs.unlink('file.txt', () => {})  
fs.mkdir('dir', () => {})  
fs.readdir('.', (e, files) => {})  
fs.stat('file.txt', (e, stat) => {})  

## Synchronous FS
fs.readFileSync('file.txt', 'utf8')  
fs.writeFileSync('file.txt', 'data')  

## Path
path.join(__dirname, 'file.txt')  
path.basename('/foo/bar.txt')  
path.extname('file.txt')  
path.resolve('file.txt')  

## HTTP Server
const http = require('http')  
const server = http.createServer((req, res) => {  
  res.writeHead(200, {'Content-Type':'text/plain'})  
  res.end('Hello World')  
})  
server.listen(3000)  

## URL
const url = require('url')  
const parsed = url.parse(req.url, true)  
parsed.query  
parsed.pathname  

## Events
const EventEmitter = require('events')  
const emitter = new EventEmitter()  
emitter.on('event', fn)  
emitter.emit('event', data)  

## Child Process
const { exec, spawn } = require('child_process')  
exec('ls', (err, stdout, stderr) => {})  
const child = spawn('node', ['app.js'])  
child.stdout.on('data', (data) => {})  

## Process
process.env.NODE_ENV  
process.argv  
process.cwd()  
process.exit(0)  
process.on('SIGINT', () => {})  
process.nextTick(fn)  

## Timers
setTimeout(fn, 1000)  
setInterval(fn, 500)  
clearTimeout(timer)  
clearInterval(timer)  

## Buffers
const buf = Buffer.from('abc')  
buf.toString('hex')  
Buffer.alloc(10)  
Buffer.concat([buf1, buf2])  

## Streams
const fs = require('fs')  
const rs = fs.createReadStream('file.txt')  
const ws = fs.createWriteStream('out.txt')  
rs.pipe(ws)  

## Crypto
crypto.createHash('sha256').update('data').digest('hex')  
crypto.randomBytes(16).toString('hex')  

## OS
os.platform()  
os.cpus()  
os.freemem()  
os.homedir()  
os.uptime()  

## Console
console.log('log')  
console.error('error')  
console.warn('warn')  
console.table(arr)  
console.time('label')  
console.timeEnd('label')  

## Packages
npm install package  
npm uninstall package  
npm update  
npm list  
npm outdated  
npm run start  
npm run build  

## Environment Variables
process.env.PORT  
process.env.USER  
require('dotenv').config()  

## Express Setup
const express = require('express')  
const app = express()  
app.get('/', (req, res) => res.send('Hello'))  
app.listen(3000)  

## Middleware
app.use(express.json())  
app.use((req,res,next) => { next() })  

## Routing
app.get('/api', fn)  
app.post('/api', fn)  
app.put('/api/:id', fn)  
app.delete('/api/:id', fn)  

## Static Files
app.use(express.static('public'))  

## JSON
JSON.stringify(obj)  
JSON.parse(str)  

## Error Handling
try { ... } catch(e) { ... }  
process.on('uncaughtException', fn)  
process.on('unhandledRejection', fn)  

## Promises
new Promise((res,rej) => {})  
promise.then().catch().finally()  
async function fn() { await bar() }  
await fetch(url)  

## Imports (ESM)
import fs from 'fs'  
import { join } from 'path'  
export default fn  
export const x = 5  

## Package.json
{  
  "name": "myapp",  
  "main": "app.js",  
  "scripts": {  
    "start": "node app.js",  
    "dev": "nodemon app.js"  
  },  
  "dependencies": {}  
}  

## Nodemon
npm install nodemon --save-dev  
npx nodemon app.js  

## Logging
console.log()  
require('debug')('app')  
require('winston').info('log')  

## Testing
npm install jest  
npm test  
describe('suite', () => { it('works', () => {}) })  

## Linting
npm install eslint  
npx eslint .  

## Module Resolution
require.resolve('module')  
module.paths  

## Versioning
node -v  
npm -v  

## REPL
node  
.global  
._  
.exit  

## Signals
process.on('SIGINT', fn)  
process.on('SIGTERM', fn)  

## Uncaught Errors
process.on('uncaughtException', fn)  
process.on('unhandledRejection', fn)  

## Application Structure
app/  
├─ app.js  
├─ routes/  
├─ controllers/  
├─ models/  
├─ views/  
├─ public/  
├─ package.json  

## Security
npm audit  
npm audit fix  
helmet  
rate limiting  
sanitize input  
validate user data  
dotenv for secrets  
escape output  

## Best Practices
Use async/await  
Handle all errors  
Limit synchronous code  
Use environment variables  
Keep dependencies updated  
Prefer const/let  
Avoid var  
Use strict mode  
Use ESLint  
Comment complex logic  
Document APIs  
Test edge cases  
Keep code modular  
Organize files  
Minimize global scope  
Use logging  
Validate input  
Escape output  
Sanitize user data  
Minimize third-party packages  
Use semantic versioning  
Monitor performance  
Keep changelog  
Automate builds  
Automate deployment  
Use CI/CD  
Limit request size  
Support HTTPS  
Use process managers  
Handle signals  
Review dependencies  
Prefer ESM  
Avoid blocking event loop  
Test with real data  
Backup regularly  
Profile memory usage  
Refactor old code  
Archive unused modules  
Version releases  
Optimize for scale  
Minimize main thread work  
Prefer stateless services  
Use error boundaries  
Keep scripts simple  
Limit permissions  
Review audit logs  
Support multiple platforms  
Test on different OS  
Automate restarts  
Monitor uptime  
Provide user feedback  
Comment intent  
Document endpoints  
Keep structure logical  
Prefer functional code  
Review security updates  
Use proper naming  
Document configuration  
Handle shutdown gracefully  
Automate testing  
Test user flows  
Monitor logs  
Keep README updated  
Document intent  
Support containers  
Validate config  
Minimize magic numbers  
