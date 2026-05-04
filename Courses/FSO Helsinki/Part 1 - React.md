# Introduction to React
- Always have `console` open.
- In JSX, every tag needs to be closed, unlike HTML.
- Pass `props` the same as you pass parameters to functions.

# Javascript
- Use `let` and `const`, ill advised to use `var`
- Const arrays's contents can still be modified, because the array itself is the same
- To add elements in array in React, it is preferable to use `arr.concat()`, which creates a new array instead of appending.
- Array methods:
	- `forEach`
	- `concat` -> creates a new array programmatically
	- `map`
- Destructuring assignments (ex. `[first, b, ...rest`)
- Objects: same as Python dicts, can be ccessed using `obj.key` or `obj[key]`
- React uses 'hooks', which makes it so that Object doesn't need to be defined with methods (we'll never use it like that.
- Calling `this` on a reference doesn't refer to the object, but a global object. `this`-less code is preferred for this reason.
- Resources to learn JS
	- [MDN JS Overview](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Language_overview)
	- [You don't know JS](https://github.com/getify/You-Dont-Know-JS)
	- [Eloquent JavaScript](https://eloquentjavascript.net)

# Component state & Event handlers
In JavaScript, defining functions inside another functions is a common practice.
- You can destructure in JS.
	```javascript
	const {name, age} = props // where props contains props.name, props.age
	// NOTE: the name of the variables must match with the props
	// You can rename using:
	const {name: userName, age} = props
	```
- Destructuring also works in the parameter declaration of a function.

**Stateful Components**
- Use the hook `useState(init_val)`.
- `useState()` returns an array with two items, `state` and `setState`.
- We use `setState` so a change in `state` value triggers a re-render.

**Event Handling**
- You can add custom handlers.
- Event handlers are functions or function references, **not** a function call.
- Ways for event handlers to take parameters:
	- Arrow functions
	- Higher-order functions (returns a function)

**Passing States to Children**
- Shared data should be moved up to the closest common ancestor.
- The same rules for passing states applies for passing event handlers to children.

# Complex-er State & Debugging React Apps
**Complex State**
- To store more complext states, you can create many different `useState()` calls, or store a single state in a certain data type. 
- A component's state can be of any type, which means you use objects inside `useState()`.
- Object spread syntax: expand array into its elements.
```javascript
{
	...directions // has to be before the overwrite
	left: left + 1, // overwrites the spreaded attribute
}
```
- Rest syntax: condense array's elements into a single variable.
- States are **immutable**, this is why you need to use `setState`.
	- For this reason, make sure use methods that creates a copy of an object (ex. `concat()` vs `push()`)
	- Also use spread to copy an object/array 
```javascript
const objcopy = {...object}
const arrcopy = [...array]
```

- Updating of the states is *asynchronous*.
- You can render components conditionally. There are many ways to do this, read [React Docs](https://react.dev/learn/conditional-rendering)
- Note: React *hooks* are new (2019), older versions use JS class syntax, learn more.

**Debugging React Apps**
- Open Console all the time.
- Use `console.log()` when debugging.
- Chrome's dev tools has a *debugger* functions, which adds breakpoints to the code.
	- To use it, go to 'Sources' tab and add `debugger` to any line to act as a breakpoint.
	- This debugger works much like vscode's debugger.
	- [Debug Javascript](https://developer.chrome.com/docs/devtools/javascript)

**Rules of Hooks**
Note: Hooks are `useState`, `useEffect`, etc.
- Hooks should only be called inside a function defining a component.
- Hooks should not be called inside loop or conditional expressions, or non component functions.

The rules above are to ensure the app runs predictably.

**Rules of Thumb**
- Do not define components inside another component.
- Open console at all times, use `console.log()` to debug.
- Progress in small steps, make sure the code works at each step.
- 

# Summary of Code
- `setInterval()`
- `useState()`
- `concat()`
- `push()`

# Dictionary
- Hooks: special Javascript function React uses to 'hook' into states. Usually have the `useX` name.