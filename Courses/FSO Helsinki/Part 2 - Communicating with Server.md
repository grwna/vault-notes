# Rendering Collections & Modules
 
 **JavaScript Arrays**
 - [Functional Programming JS](https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84)
 - `.filter()`
 - `.map()`
 - `.reduce()`
	 - `reduce` is powerful, it can replace any other array transformations.
	 - How it works, it takes 2 parameters, a callback, and a reducer variable. The callback will also have 2 parameters, one for reducer, and one for iterated value.
```javascript
array.reduce((accumulator, currentValue, currentIndex, array) => {
  // logic to update the accumulator
  // note: array is used to reference the original array
  return accumulator;
}, initialValue);
	 
```

**Rendering Collections**
- Use map to return a **new array** based on the elements from an array:
	- `notes.map(note => <li>{note.content}</li>)`
	- When rendering like this, add *key* attribute to each element.
- Note that you **should not** use array indices as keys. [Read](https://robinpokorny.com/blog/index-as-a-key-is-an-anti-pattern/). In short, indices can change for the same element.
```javascript
const sumWithInitial = array.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue,
);
```

**Modules**
- Place components in their own files in `src/components`
- Use `export default {Component}`

# Forms
Basic Syntax:
```html
<form onSubmit={handler}>
	<input />
    <button type="submit">save</button>
</form> 

```
- By default, submitting a form has many effects [Read: Submit event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event)
- To access the input's data, use controlled components
	- Add a state, then assign it as value to the form's input.
	- Add an `onChange` handler to the input (use `setState`).
		- Use `setState(event.target.value)`
	- Remember about `event.target` for event handlers.
- Use `.filter()` to create an array where every element is a subset that satisfies certain requirements.

# Fetching from Servers
- You can create a fake/mock json server with `json-server`, which will serve a json file hosted locally.
- Javascript engine follows the *asynchronous model*, which is non-blocking, because Js is single threaded.
	- Write code so that no single execution takes too long. 

**Axios and Promises**
- `axios.get()`
- Promise represents eventual completion/failure of async operations
	- It has three states, pending, fulfilled, rejected (error).
	- To access promises response, use `then`, signifying the promise was fulfilled.
	- `then` takes a callback, which is done after the eventual completion of the promise.
	- [More on promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

**Effect-hooks**
- Effects allows components connect to and synchronize with external systems. i.e. server communication.
- `useEffect(callback, deps=[array])`
- The deps (dependencies) are re run conditions, if the value inside the array changes, the effect is executed again

# Altering Data in Server
**REST**
- Data objects are called *resources*, with an address URL.
- Use `POST` to create new resource.
- axios automatically sets Content-Type headers for POST (i.e. if it's a json object.
- Use payload and response tab of Network.
- Once server data affects web app behaviour, we need to be careful with *asynchronicity* of communication.

**Updating Data**
- TIP: you can add handlers specific to certain elements when using map, by passing their `id` as parameters.
	- You can pass the handler as props for layered or deep nested components, where the handler is placed at root component.
- PUT to replace all, PATCH to change only some properties.
- axios POST, PUT returns the new data added.
- axios DELETE returns the new data added.

**Modularize Backend Fetching**
- Export Default multiple
```javascript
export default {
	getAll, create, update
}
```
- Put data fetches into a module (file), then import it.
- You can import like this `import customName from './file/path`. Then access with `customName.function`.
- **TIP**: it is better for the data fetch modules to return res.data so the components is as small as possible.
- Still be careful on how you use the data in components, you can mistakenly use it as promises instead of data.
- **BE CAREFUL WITH PROMISES** - [Promise chaining](https://javascript.info/promise-chaining)
- Invest time studying promises

**Object Definition (Segue)**
```js
const name = 'levi'
const age = 0
const person = {name, age} // this defines an object, where the key names are equal to the var names
```


**Promises and Errors**
- A fetch data that A can rename, B deletes that data. A still has the data in the client side, then renames it (modifying non existing data). What happens?
- 404 <-- but A has to open devtools to see it, the app **should not** rely on users using devtools.
- Handle gracefully <-- add `.catch()` to chain after `.then()`.
- You should add catch in the service as well as the component, use `throw error` in the service layer.
# Summary
- `.some()` (boolean) vs `.find()`(element)
- `String.includes()`
- `window.confirm('message')` <- returns boolean

> [!tip]
> If your component's handlers get too big, you can make custom hooks (more on part 7).
# Dictionary
