# Backend Structure & Intro to Testing
## Best Practices
- This section is quite lengthy, so [read](https://fullstackopen.com/en/part4/structure_of_backend_application_introduction_to_testing#project-structure)
- The structure of the project should follow some thing like this for better modularization:
```
├── controllers
│   └── notes.js
├── models
│   └── note.js
├── utils
│   ├── config.js
│   ├── logger.js
│   └── middleware.js  
├── app.js
├── index.js
```
- You can make logging better by adding this to utils
	```js
	const info = (...params) => { console.log(...params) }
	```
	- Spread is used to handle many params
	- This causes logging to be uniform, and if you have to apply specific behaviours, you can change only in one file
- Extract dotenv requiring into another file.
- Express has *routers*, which is a middleware that handles routing
	- `router = require('express').Router()`
	- Then use router to define route handlers
	- In the file with app definition, use `app.use('baseUrl', router)`
- Middleware definition can be moved to a different file
- The app definition and middleware usage (`app.use`) can beextracted to another file, where the app can be exported
	- Exporting the app means you can import it from testing modules

## Basic Testing
- Testing libraries
	- Jest: king
	- Vitest: new king
	- Node has built-in library 
		- Run with `node --test`
		- Use `{test} = require('node:test')`
		- Use `assert = require('node:assert')`
		- `node:test` executes files names `*.test.js`
		- You can group tests using `describe('name', () => {tests})`
		- [Learn more](https://nodejs.org/api/test.html)
		Example of test code:
		```js
		test('reverse of react', () => {
		  const result = reverse('react')
		  assert.strictEqual(result, 'tcaer')
		})
		```
	- Differentiate between `strictEqual` and `deepStrictEqual`
# Testing the Backend
## **Types of Tests**
- Unit tests are for small unit functions
- When you test the backend, it is not unit tests.
- When you test the backend along with the database, this is called *integraton testing*
- You can test with mock database instead of the real production database
- For mongodb, you can use `mongodb-memory-server`
##  Testing the API 
**Test Environment**
- In the package.json scripts, you can add terminal environment variables depending on whether you run prod, dev, or tests
- By doing this, you can use a different database url for testing (ideally, local db for testing).

**Supertest**
- You can use supertest to do API testing without actually doing network requests (we do not need to spin up a server for testing)
```js
const api = supertest(app)
test('notes are returned as json', async () => {
  await api
    .get('/api/notes')
	.set(any headers)
    .expect(200)
    .expect('Content-Type', /application\/json/)
})
```
- `node:test` has an after method as a cleanup function after the tests

**Database Management**
- Tests sometimes require the database to be in a certain state
- This means you have to reset the database so it's teh same each time tests are run
- This can be done using `beforeEach(()=>{})`, which runs before each test in the file/suite ('describe')
- `beforeEach` applies to the scope, for top-level, it will run alongside the suite-level calls.

**Running Tests**
- Specific tests can be run using special flags
	- Run only one test file `-- tests/file.js`
	- Run test by name (the text passed to `test('name', callback)`)
	- `-- --test-name-pattern="name-pattern"`

## Refactoring Backend for Easier Testing
- Write asynchronous code that looks synchronous
- Express will automatically call error middleware if await throws error (no need for .catch() or try-catch)
- You can create an `id` object that matches with mongodb, by saving a database object, then deleting right after, the object itself will still exis
- NOTE: `forEach()` expects synchronous functions inside it, which has a side effect that operations inside `forEach()` might not be waited on
	- To solve this you can use `Promise.all` so an array of promises gets turned to a single promise
		```js
		beforeEach(async () => {
		  await Note.deleteMany({})
		
		  const noteObjects = helper.initialNotes
		    .map(note => new Note(note))
		  const promiseArray = noteObjects.map(note => note.save())
		  await Promise.all(promiseArray)
		})
		```
	- Alternatively you can use native db operations like `insetMany`
	- Another way is using `for..of` block

> [!tip]
> Test-driven development (TDD), is the practice of implementing the tests first, before the features are implemented.

# User Administration
## Representing Data Relationships 
- Document databases traditionally do not support join queries, but MongoDB added it later.
- However, we can replicate the logic using app-level code

**References Across Collections**
- You can store references like foreign key. Ex. notes can store the id of the user who owns it OR users can store a list of all notes that they own.
- Another way is to store the notes objects themselves inside users
	- In this schema, notes are tightly nested under users and do not have default ids.
- Yet another way, is to store each other's id for both the notes and the users.
- NOSQL demands difficult design decisions, this causes it to only be suitable for a few usecases.

**Uniqueness**
- Mongoose has the `unique: bool` property as validation for uniqueness. However, the initial database state has to be healthy/clean (no duplicates).
- Violations of these returns `MongoServerError`, with `E11000 duplicate key error` message.

**Populate**
- In nosql, 'join' queries are not transactions, meaning they are not guaranteed to be consistent.
- You can join in Mongoose using `populate`, through `User.find({}).populate('notes')`
- You can then select which fields gets returned, using the syntax shown in this [documentation](https://www.mongodb.com/docs/manual/tutorial/project-fields-from-query-results/?interface=shell&language=None#return-the-specified-fields-and-the-_id-field-only).
	- Note: `id` or `_id` is always returned, and has to be suppressed using what is shown in the documentation.

## Private Data
- In mongoose you can add the `select: false` property to a schema field.
- This makes it so it doesn't get fetched by default, and has to be fetched in this way:
	```js
const user = await User.findOne({username}).select('+passwordHash');
	```

# Token Authentication
## JSON Web Tokens
**Code Syntax**
-  `jwt.sign()`
-  `jwt.verify()`
-  `bcrypt.compare()`
- `request.get()` / `request.header()`
- `string.startsWith()`
- `string.replace()`

**JWT**
- `npm add jsonwebtoken`
- There are several ways of sending tokens from browser to server
	- `Authorization` header with `Bearer` scheme
	- Cookies
	- Both of these have trade-offs between XSS vs CSRF
- The result of `jwt.verify()` is a token object, which is a javascript object., and can contain any information you want it to when creating it using `jwt.sign().  
- `jwt.verify()` will raise an error if the token being verified is missing/broken
- Additionally, you can use `express-jwt` for a middleware to validate jwts quickly. [Learn more](https://www.npmjs.com/package/express-jwt)

## Problems of Token Authentication
- API trusts tokens blindly
- For this reason, we should be able to revoke user's tokens for arbitrary reasons.
	- One way is to use expiration `jwt.sign({expiresIn: seconds})`
	- Another way is to use server-side sessions.
		- This solutions require backend database access, which is slow. Using fast db like redis is beneficial.

## More on Middlewares
- You can use middlewares on some route handlers by passing it to the handlers
	```js
	router.get('/:id', middleware, async (req, res) => {
	```
	- You can add as many middleware as possible
- You can also use it for all handlers inside a router
	```js
	app.use('/api/route', middleware, apiRouter)
	```
- 
