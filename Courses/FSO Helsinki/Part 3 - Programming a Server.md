# Node.js and Express
- To initialize basic `package.json`, use `pnpm init` or `npm init`
- Node.js runs the javascript file using the entrypoint from package.json (`index.json` by default)
- Without a framework, you need to define how to treat the request for connections.
- Example of basic server code:
```javascript
const http = require('http')

const app = http.createServer((request, response) => {
  response.writeHead(200, { 'Content-Type': 'text/plain' })
  response.end('Hello World')
})

const PORT = 3001
app.listen(PORT)
console.log(`Server running on port ${PORT}`)
```
- `response.end()` accepts string only, use JSON.stringify.

## Modules
- React uses ES6 Modules -> `import x from y`
- Node uses CommonJS Modules -> `const x = require('y')`
- Node now supports ES6, but it's not perfect.

## Express
- To Start: Express is hardcoded for Node.js, Other frameworks (like Hono) is runtime agnostic
- Package manager commands
	- `pnpm update`
	- `pnpm install`
	- `pnpm install <package>`
- Major version numbers (semantic versioning) `major.minor.patch`
	- `major` - breaking changes
	- `minor` - non breaking new features
	- `patch` - bug fixes
- Example express app:
```js
const express = require('express')
const app = express()

let notes = [ ... ]

app.get('/', (request, response) => {
  response.send('<h1>Hello World!</h1>')
})

app.get('/api/notes', (request, response) => {
  response.json(notes)
})

const PORT = 3001
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`)
}) 
```

**Express Behaviour**
- With `res.send()`, express will automatically detect the data you send and set the content type accordingly
- Alternatively, you can use `res.json()`, or other sending methods
- Keep in mind the difference between Json and Javascript Objects

 **Automatic Change Tracking**
- You can add a dev script to `package.json`:
	- `node --watch index.js`
	- Use `pnpm run dev` - needs 'run' because 'dev' is not builtin
- Alternatively, you can use `nodemon` package.

## REST
- Review:
	- Singular things (data) -> resources
	- Address of resource -> URL

**Fetching a Single Resource**
- `/api/notes/:id` -> colon (:) is for URL params in express. 
	- access the params using `req.params.<id>`
-  In express, you still need to manually define error codes (404, etc.)
	- `res.status(404).end()`
	- `end()` is to end request without sending data
	- Doing this will cause the endpoint page to not show anything (browser error), this is okay because APIs are meant to be consumed by the frontend.
- Change `res.statusMessage` to supply non-default error message

**Deleting Resources**
- Simply define a handler for the DELETE method
- NOTE: Use vscode's Bruno extension for REST client

**Receiving Data**
- `json-parser` -> `app.use(express.json())`
- This causes `req.body` to be populated with JS object based on json.

**Headers**
- Use `req.get()` to get the value of a single header
- Use `req.headers` property to see values of all headers

**Extra: Bruno and VSCode's REST Client**
- To use REST client:
	- add `requests` directory to root
	- Create `.rest` files inside, containing requests
	- Use `###` as separator to have multiple requests in one file
	- Be very wary of empty lines, this can cause errors

> [!tip]
> When working on backend code, always keep an eye on the terminal

**HTTP Request Types**
- Two important properties:
	- Safety
	- Idemptotency
- Safety: does not cause side effects in the server (ex. `GET`, `HEAD`)
- Idempotency: all requests except `POST` should be idempotent
	- Meaning, multiple requests should cause the same results, even if it causes side effects.
- **NOTE**: keep in mind that these properties are not automatic! you need to design a system with RESTful principles in mind.

## Middleware
- Functions that is used for handling `request` and `response` objects
- `json-parser` `express.json()` is a middleware
- Define middleware as a function with three parameters, `request`, `response`, and `next`. `(req, res, next)`
- Use middleware with: `app.use(middlewareFunction)`
- The order of middleware calls is the same as the order of use.
- The line where usage is defined also affects how routes use or not use the middleware.

# Deploying App to Internet
## Same Origin Policy and CORS
**Same origin policy**
- For resources fetched using URL with different origin (protocol, host, port), the browser checks `Access-Control-Allow-origin` response header.
- This is to prevent session hijacking and other vulnerabilities.

**CORS**
- To enable legitimate cross-origin requests, CORS is used.
- **Keep in mind**: CORS is configured in the backend (server)
- Use cors middleware (`app.use(cors())`)

## Application to the Internet
- PaaS with free tiers:
	- Render
	- Fly.io
- Frontend should be *built* before deployment. Using Vite, the result of building is a `dist/` folder containing the files.

**Serving Static Files from the Backend**
- You can copy the `dist/` folder into the backend root, then serve it in express using `static`
	- `express.static('dist')`
- Then GET requests to `<url>/index.html` or other files will serve the file
- You can adjust these routes in express.
- Root '/' automatically directs to `index.html` using static.

## Proxy
- In vite, you can define a proxy inside the `vite.config.js` file.
- **Example**
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],

  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:3001',
        changeOrigin: true,
      }, } }, })
```
- When the frontend's url is accessed (the `/api` endpoint), it will instead request it to `localhost:3001`, and not it's own url. Requests to sources acts normally.
- Built applications are not affected by this.

# MongoDB
**Debugging Node Applications**
- Use VSCode's debugger, or just use logging to debug.
- You can debug using Chrome dev tools by starting app with `node --inspect index.js`
- [Learn More](https://developer.chrome.com/docs/devtools/javascript)
- *Stop and Fix* - when encountering bugs, do not write more code
- In a fullstack app, bugs can come from anywhere, find the source first.

## Using MongoDB
- For complete steps of using mongodb, read the documentation or watch tutorials.
- Often, you would use an ODM (Object Data Modelling), Mongoose.

**Mongoose**
- Schema: a blueprint of a document.
	- `new mongoose.Schema({<js object definition>})`
- Model: Higher-order object constructor compiled from a schema.  
	- `const Model = mongoose.model('ModelName', modelSchema)`
	- Then to create a new document, you use `const doc = new Model({object})`
	- This new javascript object will have all of the model's properties, including all its methods.
- After operating with models, Mongoose will create a new collection automatically.
	- This collection will have the plural version of the name of the model 
	- Override this with `mongoose.model('x', y, 'collection_name')`
- Keep in Mind: this schema is application level, the collection/table itself can store multiple different schemas.

**Modifying Json of Schema**
- We can modify the schema of data returned by mongoose
- By modifying the `toJSON()` method
```js
schema.set('toJSON, {
	transform: (document, returnedObject) => {
		returnedObject.id = returnedObject._id.toString()
		delete returnedObject._id
		delete returnedObject.__v
	}
})
```

**Object Operations**
- `const obj = new Model()`
- The event handlers for these methods should call `mongoose.connection.close()`
- `obj.save().then(res)`
- `Model.find({<search filters>}).then(res)`
	- [Search Filters](https://www.mongodb.com/docs/manual/tutorial/query-documents/)
- `Model.insertMany()`

**Hidden Behaviours**
- When creating an object with `new Model()`, there is a flag  called `isNew` which is set to true
- If the object was fetched from the db, `isNew` is false
- This flag will cause `obj.save()` to either update or insert as new document

## Integrating MongoDB
**Modularizing DB Config**
- To further integrate MongoDB into the app, we should modularize the code.
- You can then export models  using `module.exports` (if using CommonJS)
- Import with `require('filepath')`
- Use `dotenv` package with `require('dotenv')`.config() to read .env

>[!TIP]
>Test backend by hitting APIs before testing through the frontend

**Error Handling**
- Requests to the database can fail, or it can return data that you don't intend for it to (like null).
- For these reasons, every external interaction (database or otherwise) should be accompanied with error handling (catch)
- Using `.then().catch()` or `try...catch` for async/await

**Error Handling Middleware**
- Sometimes, you would want to move error handling to middleware instead.
	- There are some benefits to do this, Learn More.
- To do this, pass `next` to the route handler
	- `(req, res, next)`
- Then call it in the catch block, with the argument `error`
- Error handler middleware in express are defined with four parameters instead of three `(error, req, res, next)`
- Error handler middlewares are distinguished by the parameter count. And is executed only when `next(error)` is called
- Express has a default error handler, which can be chained with your custom handler.
>[!note]
>Error Handler middleware should be defined and used at the very bottom of the code, after regular middleware and route definitions.

**Middleware Loading Order**
- Middleware are executed in the order they are used `app.use()`

# Validation and ESLint
## Validation
- You can do data validation at the mongoose level, using its schema.
```js
const schema = new mongoose.Schema({

  property1: {
    type: String,
    minLength: 5,
    required: true
  },
  property2: Boolean
})
```
- `minLength` and `required` are built-in validator, you can add [custom validator](https://mongoosejs.com/docs/validation.html#custom-validators).


## Lint
- Static analysis tools to detect errors in programming language writing, including stylistic errors.
- In Javascript, the leading linter is ESlint.
- Install ESlint with: `pnpm install eslint @eslint/js --save-dev`
- Setup with: `npx eslint --init`
- Run with: `npx eslint <index.js>`
	- Alternatively, you can add linters to the editor through extensions
- It can be configured by modifying the `eslint.config.js` file. [Learn more](https://eslint.org/docs/latest/use/configure/)
- You can add plugins to eslint to have more rules
	- Style-related rules: `@stylistic/eslint-plugin`
# Summary of Code
- `http.createServer((req, res) => {})`