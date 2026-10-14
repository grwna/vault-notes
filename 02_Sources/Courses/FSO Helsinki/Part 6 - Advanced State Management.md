In previous parts, we manage states by putting in at the top-level components and pass down as props to child components. This is fine for small scale applications, but easily becomes a burden as we scale up.

# Flux Architecture and Zustand
## Flux
An architecture used by React's own creator that puts state management outside of components, into specialized stores. States are changed through actions within the applications, which will then cause views to be re-rendered.

## Redux
Redux is a library using the flux architecture that was popular for a while. However, there are many problems with it (mainly regarding verbose code). It is now better to use Zustand instead.

## Zustand
- Use `create` to create a store
- `create` takes a function as a parameter. The function has `set` as parameter, and returns an object with the state's fields.
- `create` uses other helper functions, but only `create` itself has to be imported
- Example:
```js
import { create } from 'zustand'

const useCounterStore = create(set => ({
  counter: 0, // state initial value
  increment: () => set(state => ({ counter: state.counter + 1 
  // here, increment is an ACTION 
})), }))
```
- `set` is a function used to merge data to the stored state (look at example)
- In `set`, you can change the `increment` to something else, which would break it
- To access the states, use selectors:
```js
const counter = useCounterStore(state => state.counter)
// or
const state = useCounterStore()
const counter = state.counter
// the first method is preferred for efficiency
```
- You can also use destructuring to access fields, but this is only good for actions, and should not be used for states.
- Zustand related functions are [[Part 7 - Custom Hooks and ESBuild|custom hooks]], which means (among [[Part 1 - React#Complex-er State & Debugging React Apps|other things]]) the name has to start with `use`

**Actions Object Pattern**
- Instead of defining every actions as a direct field of the `create`\`d, you can define them under one object.
- This object can then be accessed using selectors as a whole

**Best Practices**
- Do not export the functions directly defined with `create`, divide it to smaller functions. This can make the import syntax better as well (not have to use selectors: `state => {state})`

