# Node.js / Express Guide

> _These notes are not intended as a comprehensive guide to the topic. Their purpose is to guide you through the main areas you should learn about, with resources provided for further exploration. The goal is for you to learn enough to complete the associated challenge._

## What is Node.js

- Node.js is a JavaScript runtime that lets you run JavaScript outside the browser
- Node.js is event-driven and non-blocking, meaning it can handle many simultaneous connections without waiting for each one to finish
- It is commonly used for building APIs and web servers

You can think of Node.js as a way to use JavaScript for writing back-end servers, not just front-end websites

**Further learning**
- [Node.js Official Docs](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs)
- [MDN: Introduction to Node.js](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction)

---

## Installing Node.js and npm

1. Visit [https://nodejs.org](https://nodejs.org)
2. Download and install the **LTS (Long-Term Support)** version
3. Verify installation
   ```bash
   node -v
   npm -v
   ```
4. Node.js includes **npm (Node Package Manager)**, which is used to install and manage external dependencies (libraries)

If you already have Node.js but it’s quite old, consider updating it using a version manager such as [nvm](https://github.com/nvm-sh/nvm)

---

## Running JavaScript on your computer

You can run plain JavaScript files directly with Node.js

1. Create a file called `hello.js`
   ```js
   console.log('Hello from Node.js')
   ```
2. Run it with
   ```bash
   node hello.js
   ```
3. You should see
   ```
   Hello from Node.js
   ```

This is useful for testing code, running small utilities, or learning JavaScript outside the browser


---

## Managing packages and `package.json`

When you create a Node.js project, you use a package manager to install external libraries (also known as dependencies).
Node.js comes with **npm** by default, but you can also use **yarn** or **pnpm** for similar purposes.

### Initialising a project

1. Create a new folder
   ```bash
   mkdir node-demo
   cd node-demo
   ```

2. Initialise npm
   ```bash
   npm init -y
   ```
   This creates a `package.json` file which tracks dependencies and configuration

When you run `npm init -y`, a new file called `package.json` is created. It stores information about your project and dependencies

Example:
```json
{
  "name": "demo-app",
  "version": "1.0.0",
  "main": "server.js",
  "type": "module",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {},
  "devDependencies": {}
}
```

### Key parts
- **name**: project name
- **version**: version number
- **main**: entry point file (where your app starts)
- **type**: defines whether the app uses ES modules or CommonJS
- **scripts**: shortcuts for running commands such as `npm start` or `npm test`
- **dependencies**: packages your app needs to run
- **devDependencies**: packages used only during development (for example, nodemon or testing libraries)

You can run scripts using:
```bash
npm run start
```

Run `npm install <package>` to add dependencies
Run `npm uninstall <package>` to remove them

### Installing dependencies

Install a library:
```bash
npm install chalk
```
This adds `chalk` under `dependencies` in `package.json` and creates a `node_modules` folder where it is stored

Use it in your code:
```js
import chalk from 'chalk'
console.log(chalk.green('Success'))
```

### Installing development dependencies

Development tools such as `nodemon` are usually added as dev dependencies:
```bash
npm install --save-dev nodemon
```

These are not included when the app is deployed to production.

### The `package-lock.json` file

When you install packages, npm automatically creates or updates `package-lock.json`.
This file records the exact versions installed so your project remains consistent across different machines.

### Updating and removing packages

- Update all packages to their latest safe versions:
  ```bash
  npm update
  ```
- Remove a package:
  ```bash
  npm uninstall chalk
  ```

### Common mistakes

- Committing `node_modules` to version control - it should be excluded using `.gitignore`
- Forgetting to run `npm install` when cloning a project - this installs all required dependencies

**Further learning**
- [npm Docs: About package.json](https://docs.npmjs.com/cli/v10/configuring-npm/package-json)
- [npm Docs: Working with dependencies](https://docs.npmjs.com/cli/v10/using-npm/dependency)

---

## Automatically restarting your app

When developing, you don’t want to manually restart your app every time you change a file. Tools such as **nodemon** or **ts-node-dev** automatically restart the Node process when your code changes

### Using nodemon

1. Install it globally (optional)
   ```bash
   npm install -g nodemon
   ```
   or as a local dependency
   ```bash
   npm install --save-dev nodemon
   ```

2. Add a script to `package.json`
   ```json
   "scripts": {
     "dev": "nodemon server.js"
   }
   ```

3. Start the app
   ```bash
   npm run dev
   ```

Now, every time you save a file, nodemon will restart the server automatically

**Further learning**
- [nodemon Documentation](https://github.com/remy/nodemon)

---

## ES Modules vs CommonJS

Node.js supports two import styles:

**CommonJS (older)**
```js
const express = require('express')
```

**ES Modules (modern)**
```js
import express from 'express'
```

To use ES modules, set `"type": "module"` in your `package.json`. Most new projects now use this modern format

---

## The file system

Node.js includes modules that let you read and write files directly on your computer

Example:
```js
import fs from 'fs'

fs.writeFileSync('message.txt', 'Hello Node.js')
const text = fs.readFileSync('message.txt', 'utf8')
console.log(text)
```

This is the foundation for many tasks such as creating logs or configuration files

**Further learning**
- [Node.js File System API](https://nodejs.org/api/fs.html)

---

## Creating a simple local script

Node.js can run any kind of script, not just web servers

Example: A script that prints today’s date
```js
const now = new Date()
console.log(`The current date and time is: ${now.toISOString()}`)
```

Save as `date.js` and run it:
```bash
node date.js
```

You can write automation scripts like this to handle repetitive tasks such as copying files, resizing images, or generating reports

---

## Installing dependencies and using them

You can add external packages to extend your app

Example using **chalk** to add colour to console output:

1. Install
   ```bash
   npm install chalk
   ```

2. Create a file
   ```js
   import chalk from 'chalk'
   console.log(chalk.green('Success'))
   console.log(chalk.red('Error'))
   ```

**Further learning**
- [Chalk Docs](https://github.com/chalk/chalk)

---

## Starting with Express

**Express** is a framework for building web servers and APIs in Node.js. It handles routing, middleware, and responses

### Install and create a simple server

1. Install Express
   ```bash
   npm install express
   ```

2. Create a file `server.js`
   ```js
   import express from 'express'

   const app = express()
   const port = 3000

   app.get('/', (req, res) => {
     res.send('Hello from Express')
   })

   app.listen(port, () => {
     console.log(`Server running at http://localhost:${port}`)
   })
   ```

3. Start the server
   ```bash
   node server.js
   ```
4. Visit [http://localhost:3000](http://localhost:3000)

**Further learning**
- [Express Getting Started Guide](https://expressjs.com/en/starter/installing.html)

---


## Routing and API endpoints

Routing defines how your server responds to different URLs and HTTP methods.

Each route represents a different path clients can request data from or send data to. For example, a front-end app might request `/planets` to get a list of planets, `/planets/1` to get a specific planet, or send data to `/planets` to add a new one.

This separation of routes allows your API to handle multiple types of client requests in an organised way.

Example:
```js
app.get('/planets', (req, res) => {
  res.json([{ id: 1, name: 'Earth' }, { id: 2, name: 'Mars' }])
})

app.get('/planets/:id', (req, res) => {
  const planetId = parseInt(req.params.id)
  const planet = { id: planetId, name: 'Earth' }
  res.json(planet)
})

app.post('/planets', (req, res) => {
  const planet = req.body
  res.status(201).json({ message: 'Planet created', planet })
})
```

### Returning data types

Express can return plain text, HTML, or JSON objects. JSON is most common for APIs because it’s easy to use with JavaScript on the front-end.

Examples:
```js
// Plain text
res.send('Hello from Express')

// JSON
res.json({ message: 'Data received successfully' })

// Custom status codes
res.status(404).json({ error: 'Planet not found' })
```

**Further learning**
- [Express Routing Guide](https://expressjs.com/en/guide/routing.html)

---

## Serving static files

Sometimes you’ll want to serve static files like images, CSS, or JavaScript directly from your server. Express provides a simple built-in middleware for this.

Example:
```js
import express from 'express'
const app = express()

// Serve files from the 'public' directory
app.use(express.static('public'))

app.listen(3000, () => console.log('Server running on port 3000'))
```

Now, any file placed inside the `public` folder (for example `public/index.html` or `public/styles.css`) will be served automatically when requested by a client.

This is useful for serving documentation, static front-end assets, or uploads.

**Further learning**
- [Express Static Middleware](https://expressjs.com/en/starter/static-files.html)

---

## Using try/catch and handling internal errors

When working with asynchronous code (e.g. database calls or external APIs), you should always use `try/catch` blocks to handle unexpected errors.

Example:
```js
app.get('/data', async (req, res) => {
  try {
    const data = await fetchDataFromDatabase()
    res.json(data)
  } catch (error) {
    console.error('Error fetching data:', error)
    res.status(500).json({ error: 'Internal server error' })
  }
})
```

### Why this matters

If your server fails to handle an error, it can crash or leave clients hanging without a response. A 500 status code (`Internal Server Error`) signals to the client that something went wrong on the server side.

In production, instead of using `console.error`, errors should be logged properly to a logging service such as Sentry for later review.

Using error handling and logging ensures your API behaves predictably and safely even when things go wrong, and allows you to monitor issues.

---

## Middleware

Middleware are functions that run between receiving a request and sending a response. They are used for tasks such as parsing JSON, logging, authentication, and error handling

### Example
```js
app.use(express.json())

app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`)
  next()
})
```

Middleware runs in order, so put general-purpose ones (like logging) before routes

**Further learning**
- [Express Middleware Guide](https://expressjs.com/en/guide/using-middleware.html)

---

## Environment variables

Store settings and credentials outside your code, such as API keys and database URLs

1. Install dotenv
   ```bash
   npm install dotenv
   ```

2. Create a `.env` file
   ```
   PORT=4000
   ```

3. Load it in your code
   ```js
   import dotenv from 'dotenv'
   dotenv.config()

   const port = process.env.PORT || 3000
   app.listen(port, () => console.log(`Server running on port ${port}`))
   ```

**Further learning**
- [dotenv Docs](https://github.com/motdotla/dotenv)

---

## Cookies

Cookies store small bits of data in the browser, such as session information

1. Install cookie-parser
   ```bash
   npm install cookie-parser
   ```

2. Use it in your app
   ```js
   import cookieParser from 'cookie-parser'
   app.use(cookieParser())

   app.get('/set-cookie', (req, res) => {
     res.cookie('theme', 'dark')
     res.send('Cookie set')
   })

   app.get('/read-cookie', (req, res) => {
     res.send(`Theme: ${req.cookies.theme}`)
   })
   ```

**Further learning**
- [cookie-parser Docs](https://www.npmjs.com/package/cookie-parser)

---

## CORS (Cross-Origin Resource Sharing)

CORS allows your front-end app (running on a different port) to make API calls to your back-end

1. Install
   ```bash
   npm install cors
   ```

2. Use it
   ```js
   import cors from 'cors'
   app.use(cors({ origin: 'http://localhost:5173' }))
   ```

**Further learning**
- [MDN: CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
[Express - CORS](https://expressjs.com/en/resources/middleware/cors.html)

---

## Connecting to a database

You can connect to databases with Node.js. The example below uses PostgreSQL:

1. Install `pg`
   ```bash
   npm install pg
   ```

2. Example connection
   ```js
   import pkg from 'pg'
   const { Pool } = pkg

   const pool = new Pool({
     connectionString: process.env.DATABASE_URL
   })

   const result = await pool.query('SELECT NOW()')
   console.log(result.rows)
   ```

**Further learning**
- [node-postgres Docs](https://node-postgres.com/)

---

## Handling errors

Express provides built-in tools for handling errors. Use middleware for consistency

```js
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).json({ error: 'Something went wrong' })
})
```

For async handlers:
```js
app.get('/example', async (req, res, next) => {
  try {
    const data = await someFunction()
    res.json(data)
  } catch (err) {
    next(err)
  }
})
```

**Further learning**
- [Express Error Handling](https://expressjs.com/en/guide/error-handling.html)

---

## Folder structure

As your app grows, organise files for clarity

Example:
```
project/
│
├── server.js
├── routes/
│   └── planets.js
├── middleware/
│   └── logger.js
├── db/
│   └── index.js
├── .env
└── package.json
```

Keep each concern in its own folder

---

## Putting it all together

```js
import express from 'express'
import cors from 'cors'
import dotenv from 'dotenv'

dotenv.config()
const app = express()
const port = process.env.PORT || 4000

app.use(cors())
app.use(express.json())

app.get('/', (req, res) => {
  res.send('Welcome to the Space API')
})

app.get('/planets', (req, res) => {
  res.json([
    { id: 1, name: 'Earth' },
    { id: 2, name: 'Mars' },
  ])
})

app.listen(port, () => console.log(`Server running on port ${port}`))
```

Run with:
```bash
npm run dev
```

---

## Further learning

- [Express.js Official Guide](https://expressjs.com/en/guide/routing.html)
- [MDN: Express and Node Basics](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
- [CORS on MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [The Modern JavaScript Tutorial: Modules](https://javascript.info/modules-intro)
