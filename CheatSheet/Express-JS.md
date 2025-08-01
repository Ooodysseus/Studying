# Express JS Cheatsheet

## Basics
const express = require('express')
const app = express()
const PORT = process.env.PORT || 3000
app.listen(PORT, () => console.log(`Server running on port ${PORT}`))

## Routing
app.get('/', (req, res) => res.send('Hello World'))
app.post('/user', (req, res) => { /* ... */ })
app.put('/user/:id', (req, res) => { /* ... */ })
app.delete('/user/:id', (req, res) => { /* ... */ })

## Route Parameters & Query
app.get('/user/:id', (req, res) => res.send(req.params.id))
app.get('/search', (req, res) => res.send(req.query.q))

## Middleware
app.use(express.json())
app.use(express.urlencoded({ extended: true }))
app.use((req, res, next) => { console.log(req.method, req.url); next() })

## Static Files
app.use(express.static('public'))

## Error Handling
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})

## Custom Middleware
function logger(req, res, next) {
  console.log(`${req.method} ${req.url}`)
  next()
}
app.use(logger)

## Chained Routes
app.route('/book')
  .get((req, res) => { /* ... */ })
  .post((req, res) => { /* ... */ })
  .put((req, res) => { /* ... */ })

## Request & Response
req.body
req.params
req.query
req.headers
res.status(200).send('OK')
res.json({ ok: true })
res.redirect('/other')
res.end()

## 404 Handler
app.use((req, res) => {
  res.status(404).send('Not found')
})

## Project Structure
project/
  ├─ app.js
  ├─ routes/
  ├─ controllers/
  ├─ models/
  ├─ middleware/
  ├─ public/
  ├─ package.json

## Router
const router = express.Router()
router.get('/users', (req, res) => { /* ... */ })
app.use('/api', router)

## Environment Variables
require('dotenv').config()
process.env.PORT

## Cookies & Sessions
const cookieParser = require('cookie-parser')
app.use(cookieParser())
req.cookies
res.cookie('token', 'value')

const session = require('express-session')
app.use(session({ secret: 'key', resave: false, saveUninitialized: true }))

## CORS
const cors = require('cors')
app.use(cors())

## Helmet (Security)
const helmet = require('helmet')
app.use(helmet())

## File Uploads (multer)
const multer = require('multer')
const upload = multer({ dest: 'uploads/' })
app.post('/upload', upload.single('file'), (req, res) => res.send('Uploaded!'))

## Validation (express-validator)
const { body, validationResult } = require('express-validator')
app.post('/register', body('email').isEmail(), (req, res) => {
  const errors = validationResult(req)
  if (!errors.isEmpty()) return res.status(400).json({ errors: errors.array() })
})

## Logging (morgan)
const morgan = require('morgan')
app.use(morgan('dev'))

## API Response
res.json({ message: 'Hello' })
res.status(201).json({ created: true })
res.sendStatus(404)
res.setHeader('Content-Type', 'application/json')

## Async/Await
app.get('/async', async (req, res) => {
  try {
    const data = await fetchData()
    res.json(data)
  } catch (err) {
    res.status(500).send(err.message)
  }
})

## Database Example (Mongo/Mongoose)
const mongoose = require('mongoose')
mongoose.connect(process.env.MONGO_URL)
const User = mongoose.model('User', { name: String })
app.get('/users', async (req, res) => res.json(await User.find()))

## Nested Routers
const postsRouter = require('./routes/posts')
app.use('/posts', postsRouter)

## Sending Files
res.sendFile(__dirname + '/public/file.pdf')

## Redirects
res.redirect('/home')

## Download
res.download('./files/report.pdf')

## Request Methods
req.method
req.url
req.get('header-name')

## Response Methods
res.status(200)
res.set('X-Header', 'value')
res.type('json')
res.cookie('token', 'xyz')
res.clearCookie('token')

## Chain Middleware
app.get('/profile', authMiddleware, profileMiddleware, (req, res) => { /* ... */ })

## Best Practices
Structure code with routes/controllers/models
Use environment variables for secrets
Validate all data from clients
Handle errors and edge cases
Limit synchronous code in endpoints
Keep middleware modular
Document APIs and endpoints
Log requests and errors
Automate builds, tests, and deploys
Use helmet and CORS for security
Update dependencies regularly
Optimize for performance and scalability
Archive unused code
Test user flows and edge cases
Keep README and changelog up to date
Refactor old code
Prefer async/await
Use separate config files
Prefer composition over inheritance
Comment intent and complex logic
Lint code
Use version control
Backup configs
Automate deployment
Monitor performance and logs
Support containers and CI/CD
Prefer functional code
Version releases

