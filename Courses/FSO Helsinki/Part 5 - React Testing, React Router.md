# Review
- To create forms, add states that represents the values of the form.
- Event handlers use targets, destructure the target from the object.
```js
({ target }) => setUsername(target.value)
```
- Putting input/forms inside labels. `<label>Name <input></input></label>`
- Remember global variables
- Flow of component based UI design:
	- Prototype UI inline: allows for quick prototyping
	- Extract intoo a separate component
	- Derive props based on the prototype
	- This flow allows you to prototype quickly without having to think about what props to put where in the beginning.

# Frontend-side Auth
- Set headers in `axios` using the third arguments `axios.post(url, data, headers)`
- To persist credentials, we can use the browser's local storage.
	- `window.localStorage.setItem('key', 'value')`
	- `window.localStorage.getItem('key')`
	- `window.localStorage.removeItem('key')`
- Local storage stores DOMstrings, not Js object. So use `JSON.stringify` to store, then parse with `JSON.parse`a
- NOTE on security: since storing in localStorage has a risk of XSS, you need to minimize XSS vectors in the application.

# Component Refs & props.children
- To use `&&` or `display` for conditional rendering?
	- `&&` are usually preferred
- You can add elements inside the tags for components. 
- These 'children' can be accessed by using the component's `props`, with `props.children` from inside the component's code
- `props.children` always exists in react, defaulting to an empty array.

**State of the Forms**
- Lifting state up: 
	>*Sometimes, you want the state of two components to always change together. To do it, remove state from both of them, move it to their closest common parent, and then pass it down to them via props.*

**Refs**
- One usage of refs is to call a component's function from it's parent component.
- You use an imperative handle using `useImperativeHandle` inside the component to 'expose' the function to the parent component.
- The parent component defines a `useRef`, which will become the reference to the child component. You pass this ref to the child component with `<Comp ref={definedRef}/>`
- Then call the function using `definedRef.current.functionName()`.
- The ref refers to one *specific instance* of a component.


# Testing React Apps
- This section will not be explained in detail, as they are mostly technical details instead of concepts. [Read](https://fullstackopen.com/en/part5/testing_react_apps).
- Libraries:
	- vitest: the base testing framework
	- jsdom: simulate browser
	- react-testing-library: for rendering react components
		- `npm install --save-dev @testing-library/react @testing-library/jest-dom`
		- react
		- jest-dom
	- user-event: simulate user input like clicking buttons
- You an access components in the tests using elements's class names.
	- Uses `querySelector`
	- However, it is recommended to use anything other than these. Use something like `getByText` instead.
	- Note that query selector works for all CSS selectors, including ids, etc.
- You can store test files in multiple ways, one way is to store them in the `components` directory, another way is to store in `tests` directory.
- Use `vi.fn()` a function that provides mocks (to call `mock.calls`, etc.)

**Selecting Elements**
- **`getByRole`** – Finds elements by semantic role and accessible name (e.g., `button`, `heading`). **(Recommended First Choice)**
- **`getByLabelText`** – Finds form input elements by their associated `<label>` text.
- **`getByPlaceholderText`** – Finds input fields using their placeholder text value.
- **`getByText`** – Finds static text content (e.g., paragraphs, spans, divs).
- **`getByDisplayValue`** – Finds form fields by their current populated value.
- **`getByAltText`** – Finds images or areas using their `alt` text attribute.
- **`getByTitle`** – Finds elements using their `title` attribute (common for SVGs).
- **`getByTestId`** – Finds elements using a dedicated `data-testid` attribute. **(Fallback Only)**run 

**Coverage**
- You can view the tests coverage for components using `vitest run -- -- coverage`
- This will print the coverage in the console, and also generates an HTML report that shows the lines of untested code.

**Snapshot Testing**
- Vitest has snapshot testing, where the developers does not have to define the tests themselves. [Learn more](https://vitest.dev/guide/snapshot)

# End to End Testing
- E2E a.k.a. System testing
- Most useful test -> use the same interface as real users
- E2E can be expensive, so running tests repeatedly during development is not feasible.
- E2E can be flaky -> pass one time, fail another time, no code changes.
- Libraries: Selenium, Cypress, Playwright
	- Cypress -> entirely on browser
	- Playwright -> node process, using API to connect to browser
- Playwright will be the focus for this course
- E2E tests does not need to be in the same directory as the project being tested.

## Playwright
Since there is a lot of details to cover, it is better to read the documentations instead of relying on notes. [Playwright docs](https://playwright.dev/docs/intro)
- Installation
	- `npm init playwright@latest` 
	- `pnpm dlx create-playwright`
- Basic commands
	- `playwright test`
    - `playwright show-report`
    - `playwright test --ui`
- E2E test requires each component (FE, BE) to be started manually. Using the development mode (`--watch`) with test environment is desired.
- The base test structure are the same as other testing frameworks, with describe and test blocks, and expect
- Playwrights waits for elements to show up for 5 to 30 seconds, until it times out.
	- This causes failed tests to be slower than successes
	- It might be beneficial to reduce timeout
- Playwright uses parallel execution by default, this can cause problems with database access.
- When locating elements, utilize content visible to the users (text, labels, etc.), as this best simulates the user's experience.
- Each tests runs from browser's 'zero' state
- You can run specific or only one test at a time

**Config**
- You can set timeouts, parallelization, baseURLs in the config file

**CSS**
- `page.locator([css selectors/XPath selectors])`
- `expect().toHaveCSS(style definitions)`

**Controlling Database States**
- E2E has no access to database (simulates user)
	- Create custom testing apis in the backend.
- Playwright can call API directly using `request`
- NOTE: Playwright uses injection based on parameter names. 
	- This means, the exact parameter name (`page`, `request`) is important.
- You can force tests to wait for a component to render using `.waitFor()`
	- `await page.getByText("test").waitFor()`, waits for 
	  "test" to appear on screen.

**Debug**
- Commands
	- `playwright test -g'test name' --debug`
	- `playwright test --trace on
		- Access trace using show-report
- Playwright's debugger is a full blown debugger with step by step capabilities.
- Add a breakpoint using `await page.pause()` in the test code


# React Router, UI Frameworks
## React Router
- React uses SPA, only one page with illusion of multiple pages through javascript.
- You can simulate different pages by conditionally rendering them based on a page state
	- url remains the same, so it's not optimal
	- Back buttons won't work
- React Router is the solution for managing React navigation `react-router-dom`
- Uses `BrowserRouter`, `Routes`, `Route`, `Link`
	- `Link` is for creating links (like `<a>`)
	- `Routes` is the block in which `Route` are placed
	- `BrowserRouter` is the parent element for every component that is intended to be routed
	
```js
import {
  BrowserRouter as Router,
  Routes, Route, Link
} from 'react-router-dom'
  
  return (
    <Router>
      <div>
        <Link style={padding} to="/">home</Link>
        <Link style={padding} to="/notes">notes</Link>
        <Link style={padding} to="/create">new note</Link>
      </div>

      <Routes>
        <Route path="/notes" element={
          <NoteList notes={notes} />
        } />
        <Route path="/create" element={
          <NoteForm createNote={addNote}/>
        } />
        <Route path="/" element={<Home />} />
      </Routes>
    </Router>
  )
}
export default App
```
- Note: `Link` can be used anywhere
- Note: the `Router` or `BrowserRouter` is usually used directly in `Main.jsx`, wrapping `App.jsx`
## Parameterized Route
- You can use parameters in urls
- In `Link`, write like this: `<Link to={'/notes/${note.id}'}></Link>`
- In `Route`, use `<Route path="/notes/:id">` as a different `Route` instance from the one with `/notes`
- In order for components to use the id, use `useParams().id` (where id can be anything)
	- The `id` here is mapped by React Router when you define `Route path='/:params'`
- Note: the `Router` or `BrowserRouter` is usually used directly in `Main.jsx`, wrapping `App.jsx`

is this statement incorrect?

**useNavigate**
- `useNavigate` is used to automatically navigate the user to another page, for example, as a consequence of certain actions.
- `useParams`, `useNavigate` are hooks and follow the rules that hooks abide by.

**useMatch**
- `useMatch` allows to bind values of parameters into the parent component.
- This allows the parent component to resolve the element to render to a component, meaning the component does not have to be passed an array of list, only to find the id inside.
- `useMatch` cannot be used directly inside a component taht uses the `BrowserRouter`, so move the `BrowserRouter` a level higher.
- Use by using `const match = useMatch('/notes/:id')`, and when you visit the page with parameters, the `match` variable will have a value.
	- The params can be accessed using `match.params.id`

## UI Libraries: Material
- One of the most popular all-in-one UI libraries is [MaterialUI](https://mui.com/), which implements Google's Material Design.
	- `npm install @mui/material @emotion/react @emotion/styled`

**How to use MUI**
- `<Container>` - wrap app's entire content within a container component

**MUI Components**
- Import with `import {} from '@mui/material'`
- Table
	- `TableContainer`
	- `Table`
	- `TableHead`
	- `TableBody`
	- `TableRow`
	- `TableCell`
- Form
	- `TextField`
	- `Button`
- Notifications
	- `Alert`
- Navigation
	- `AppBar`
	- `Toolbar`
	- `<Button component={Link} to="/">`

## UI Libraries: Styled Components
![[Pasted image 20260724220808.png|500]]
 - `styled-components` can be used to define CSS within javascript using ES6's tagged template literal.
 - Example:
 ```js
import styled from 'styled-components'
const Button = styled.button`
  background: Bisque;
  font-size: 1em;
  margin: 1em;
`
const Input = styled.input`
  margin: 0.25em;
  width: 300px;  
`
 ```
 - `Button` and `Input` are button and input HTML elements respectively, which are bundled with the style. The elements themselves act as the original elements.
 - By using `styled-components`, you achieve full css capabilities, and some other benefits (learn more) compared to inline styling
 - There are tradeoffs though, for example, `styled-components` rely on runtime JS evaluation