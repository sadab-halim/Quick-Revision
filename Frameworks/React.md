<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# You are a React expert and mentor.

Your task is to generate a structured **quick revision notes for interview preparation** on React, broken into sections.  
I will specify which section to start from, and you will cover ONLY that section in detail.

### Output Rules:

- Be concise, yet cover all the concepts, revision notes should be crisp and clear.
- Use headings, bullet points, tables, and short code snippets.
- Highlight **common pitfalls**, **best practices**, and **React version notes** (React 18+ and React 19).
- Use comparison tables where useful (e.g., class components vs function components, useEffect vs useLayoutEffect).
- Include **short real-world examples** (JSX snippets, hooks, context usage).
- For complex or abstract topics (e.g., reconciliation, concurrent rendering, hooks rules), use **real-life analogies**.
- End each section by asking if I want to continue with the next one.


### Sections:

1. React Fundamentals (JSX, components, props, state, virtual DOM)
2. State Management (local state, Context API, Redux, Zustand, Recoil, Jotai)
3. Component Lifecycle \& Hooks (useState, useEffect, useMemo, useCallback, useReducer, useLayoutEffect)
4. Routing (React Router, nested routes, dynamic routing)
5. Forms in React (controlled/uncontrolled, validation, Formik, React Hook Form)
6. React Rendering and Reconciliation (diffing algorithm, keys, re-render triggers)
7. Performance Optimization (memoization, lazy loading, code splitting, Suspense)
8. Advanced Patterns (render props, HOCs, custom hooks, compound components)
9. Portals \& Error Boundaries (use cases, fallback UI, error handling)
10. Refs and DOM Manipulation (useRef, forwardRef, imperative handles)
11. React with TypeScript (props typing, hooks typing, generics, utility types)
12. React with Backend APIs (fetch, Axios, React Query, SWR, GraphQL)
13. Styling in React (CSS modules, styled-components, Tailwind, Emotion)
14. Accessibility (A11y) (ARIA roles, keyboard navigation, screen readers)
15. Internationalization (i18n) (react-intl, i18next, formatting)
16. Testing (Jest, React Testing Library, Cypress, mocking APIs)
17. Server-Side Rendering \& Streaming (Next.js, hydration, React 18 streaming APIs)
18. React 18+ and 19 Features (concurrent rendering, transitions, use hook family, server components)
19. React + Web Workers (offloading heavy tasks, Comlink, workerize)
20. Error \& Performance Diagnostics (React DevTools, profiling, logging, Sentry)
21. Folder Structure \& Anti-Patterns (scalable structures, avoiding prop drilling, antipatterns like deeply nested state)
22. Ecosystem Awareness (Next.js, Remix, Gatsby, Expo, Vite, Astro, React Native basics)

### Instruction:

When I say **"Start from Section X"**, generate the revision guide for that section only.  
When done, ask me if I want to continue with the next section.  
Always maintain the same style so the entire revision guide feels consistent.

I am ready. Please let me know which section you would like to start with.

---

# Start from Section: 1

React fundamentals cover the core concepts of building user interfaces with components, props, state, and JSX, all optimized through the Virtual DOM. These building blocks are essential for creating dynamic and efficient web applications.

### JSX (JavaScript XML)

JSX is a syntax extension for JavaScript that allows you to write HTML-like code within your JavaScript files. It is compiled by tools like Babel into standard `React.createElement()` calls.

* **Key Features:**
    * It combines UI logic and rendering logic in one place (components).
    * You can embed JavaScript expressions inside JSX using curly braces `{}`.
    * HTML attributes are written in **camelCase**, for example, `className` for the `class` attribute and `onClick` for the `onclick` event.
    * All JSX elements must be wrapped in a single parent element. You can use a **React Fragment** (`<>...</>`) to avoid adding an extra node to the DOM.

```jsx
// Example of JSX
function Greeting({ name }) {
  const user = { firstName: 'John', lastName: 'Doe' };
  
  return (
    <>
      <h1>Hello, {name}!</h1>
      <p>Your full name is {user.firstName} {user.lastName}.</p>
    </>
  );
}
```

* **Common Pitfall:** Returning multiple adjacent elements without a wrapper, which causes a syntax error.


### Components

Components are independent, reusable pieces of UI. They are like JavaScript functions that return React elements.


| Feature | Functional Components | Class Components |
| :-- | :-- | :-- |
| **Syntax** | Simple JavaScript functions. | ES6 classes extending `React.Component`. |
| **State** | Managed with the `useState` and `useReducer` hooks. | Managed with `this.state` and `this.setState()`. |
| **Lifecycle** | Managed with the `useEffect` hook. | Managed with lifecycle methods (e.g., `componentDidMount`). |
| **`this` Keyword** | Not used. `props` are passed as arguments. | `this` is used to access props and state. |
| **Modern Usage** | **Recommended standard** for all new development. | Legacy; still found in older codebases. |

* **Best Practice:** Use functional components with hooks as they lead to more concise and readable code.

```jsx
// Functional Component Example
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```


### Props (Properties)

Props are read-only objects used to pass data from a parent component to a child component. This flow of data is unidirectional (one-way).

* **Analogy:** Props are like arguments passed to a function. The component receives them and uses them to render the UI, but it cannot change them.
* **Common Pitfall:** Trying to modify props directly in a child component (e.g., `props.name = 'New Name'`). This is an anti-pattern. If a child needs to modify a value, the parent should pass down a callback function that modifies the state in the parent.

```jsx
// Parent Component
function App() {
  return <UserProfile name="Alex" age={30} />;
}

// Child Component
function UserProfile(props) {
  return <p>{props.name} is {props.age} years old.</p>;
  // Do NOT do this: props.age = 31;
}
```


### State

State is data that a component manages internally. When the state changes, React automatically re-renders the component to reflect the new state.

* **Analogy:** State is a component's private memory. It can update its own memory, and when it does, it may decide to look or act differently.
* The `useState` hook is the primary way to manage state in functional components. It returns an array with two elements: the current state value and a function to update it.

```jsx
const [value, setValue] = useState(initialValue);
```

* **Best Practice:** Updates to state are asynchronous. React may batch multiple `setState` calls into a single re-render for performance.


### Virtual DOM (VDOM)

The Virtual DOM is a programming concept where a virtual representation of a UI is kept in memory and synced with the "real" DOM.

* **Reconciliation Analogy:** Imagine you have a blueprint of a house (the VDOM). When you want to make a change, you first edit the blueprint (create a new VDOM). Then, you compare the new blueprint to the old one to find the differences. Finally, you send a list of minimal, specific instructions to the construction crew (updating the real DOM) instead of rebuilding the entire house.
* **Process:**

1. When a component's state changes, React creates a new VDOM tree.
2. This new tree is compared ("diffed") with the previous VDOM tree.
3. React calculates the most efficient way to apply these changes to the real DOM.
4. The changes are batched and updated in the real DOM, minimizing costly DOM manipulations.
* **React 18+ Note:** Automatic batching is a key feature. Previously, React only batched updates within its own event handlers. Now, updates inside `setTimeout`, promises, or native event handlers are also batched automatically, leading to fewer re-renders and better performance.

***

Would you like to continue with Section 2: State Management?

---

# yes

Of course. Here is the quick revision guide for Section 2.

### State Management

State management in React is about how you store and update the data that your application uses. The right strategy depends on the complexity of your application and where the data is needed.

#### Local State vs. Global State

* **Local State:** Data that is only needed by a single component or a small part of the component tree. The `useState` and `useReducer` hooks are perfect for this.
* **Global State:** Data that needs to be accessed by multiple components across different parts of the application (e.g., user authentication status, theme).

**Best Practice:** Start with local state. Only move state "up" to a shared ancestor or to a global store when multiple components need to share it. This avoids unnecessary complexity.

***

### Techniques for State Management

#### 1. Lifting State Up

This is the most basic way to share state between components. If two child components need to share the same data, you move the state to their closest common parent. The parent then passes the state down as props and the update function as a callback.

* **Common Pitfall:** Can lead to "prop drilling," where props are passed through many layers of components that don't need them.

```jsx
// Parent component holding the state
function Parent() {
  const [value, setValue] = useState('');

  return (
    <>
      <Input value={value} onValueChange={setValue} />
      <Display value={value} />
    </>
  );
}

// Child components receiving state and callbacks
const Input = ({ value, onValueChange }) => (
  <input value={value} onChange={(e) => onValueChange(e.target.value)} />
);

const Display = ({ value }) => <p>Current value: {value}</p>;
```


#### 2. Context API

The Context API is React's built-in solution for avoiding prop drilling. It allows you to pass data through the component tree without having to pass props down manually at every level.

* **Analogy:** Think of the Context API as a public announcement system for a building. The `Provider` makes an announcement from the top floor (e.g., "The theme is now 'dark'"). Any component in the building with a receiver (`useContext`) can hear this announcement directly, without having to pass the message down through every floor.
* **Core APIs:**
    * `React.createContext()`: Creates a Context object.
    * `<MyContext.Provider value={...}>`: Provides the value to all components nested inside it.
    * `useContext(MyContext)`: A hook that lets a component subscribe to the context value.

```jsx
// 1. Create a context
const ThemeContext = React.createContext('light');

// 2. Provide the context value
function App() {
  const [theme, setTheme] = useState('dark');
  
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

// 3. Consume the context value
function ThemedButton() {
  const { theme, setTheme } = useContext(ThemeContext);
  
  return (
    <button 
      style={{ background: theme === 'dark' ? '#333' : '#FFF' }}
      onClick={() => setTheme(theme === 'dark' ? 'light' : 'dark')}
    >
      Toggle Theme
    </button>
  );
}
```

* **Common Pitfall:** When the `value` of the `Provider` changes, **all** components that consume that context will re-render. This can cause performance issues if not managed carefully with `useMemo` or by splitting contexts.


#### 3. Third-Party State Management Libraries

For complex applications, dedicated libraries offer more powerful features like middleware, devtools, and optimized performance.


| Library | Core Concept | Boilerplate | Learning Curve | Best For |
| :-- | :-- | :-- | :-- | :-- |
| **Redux** | Single immutable global store ("Single Source of Truth"). Changes happen via dispatched actions and pure reducer functions. | High | Steep | Large, complex apps with predictable state changes (e.g., enterprise dashboards). |
| **Zustand** | Minimalist, un-opinionated store based on hooks. State is mutable, like in vanilla JavaScript. | Very Low | Easy | Small to large apps where you want simplicity and less boilerplate than Redux. |
| **Recoil** | "Atomic" state. State is broken into independent pieces (`atoms`) that components can subscribe to. | Low | Moderate | Apps where components only need to subscribe to small, specific pieces of state, avoiding large re-renders. Developed by Facebook. |
| **Jotai** | Similar to Recoil (atomic state), but with an even more minimalist, bottom-up approach. | Very Low | Easy | Similar to Recoil and Zustand; a great lightweight alternative. |

* **React 18+ Note:** These libraries now use the `useSyncExternalStore` hook internally. This is a special hook provided by React that allows external stores to integrate safely with concurrent features, ensuring UI consistency during rendering. You won't use it directly, but it's a key reason why these libraries work so well with React 18+.

***

Would you like to continue with Section 3: Component Lifecycle \& Hooks?

---

# yes

Of course. Let's dive into Section 3.

### Component Lifecycle \& Hooks

In modern React, we use **Hooks** to manage a component's lifecycle and state within functional components. Hooks are functions that let you "hook into" React state and lifecycle features.

#### From Class Lifecycle to Hooks

Hooks simplify the complex lifecycle methods of class components into a more unified API.


| Class Lifecycle Method | Hook Equivalent in Functional Components | Use Case |
| :-- | :-- | :-- |
| `constructor` | `useState` or `useReducer` initial state. | Initializing state. |
| `componentDidMount` | `useEffect(() => { ... }, [])` | Running a side effect once after the initial render. |
| `componentDidUpdate` | `useEffect(() => { ... }, [dep1, dep2])` | Running a side effect whenever a dependency changes. |
| `componentWillUnmount` | `useEffect(() => { return () => { ... } }, [])` | Cleaning up a side effect before the component is removed. |


***

### Key Hooks Explained

#### 1. `useState`

The most fundamental hook. It lets you add state to a functional component.

* **Syntax:** `const [state, setState] = useState(initialValue);`
* **Best Practice:** When the new state depends on the previous state, use the functional update form to ensure you have the latest state.

```jsx
// Good: Functional update
setCount(prevCount => prevCount + 1);

// Bad: Can lead to race conditions if updates are batched
setCount(count + 1);
```


#### 2. `useEffect`

This hook is for performing **side effects**: data fetching, subscriptions, or manually changing the DOM.

* **Analogy:** `useEffect` is like setting up a subscription. You tell React: "Whenever *this thing* (a dependency) changes, run *this action* (the effect). And here’s how to *cancel the subscription* (the cleanup function) when it's no longer needed."
* **The Dependency Array is Crucial:**
    * `[]` (empty array): The effect runs **only once**, after the first render (like `componentDidMount`).
    * `[dep1, dep2]`: The effect runs after the first render **and** any time `dep1` or `dep2` changes.
    * **No array**: The effect runs after **every single render**. **Common Pitfall:** This often leads to infinite loops if the effect itself triggers a state update.

```jsx
// Example: Fetching data on mount and cleaning up
useEffect(() => {
  const controller = new AbortController();
  const signal = controller.signal;

  fetch('https://api.example.com/data', { signal })
    .then(res => res.json())
    .then(setData);

  // Cleanup function: runs when component unmounts or before the effect re-runs
  return () => {
    controller.abort(); // Cancel the fetch request
  };
}, []); // Empty array means this runs only once
```

* **React 18+ Note:** In Strict Mode (during development), React will mount, unmount, and then re-mount components. This means your `useEffect` will run twice on the initial render, with the cleanup function running in between. This is intentional to help you find bugs related to improper cleanup.


#### 3. `useMemo`

Memoizes the result of an expensive calculation. The function is re-executed only when one of its dependencies changes.

* **Use Case:** Preventing costly re-calculations on every render, such as filtering a large list.

```jsx
const visibleTodos = useMemo(
  () => filterTodos(todos, tab),
  [todos, tab] // Only re-calculate if 'todos' or 'tab' changes
);
```

* **Common Pitfall:** Overusing `useMemo` for simple calculations. The overhead of memoization can be more expensive than the calculation itself. Use it for genuinely heavy computations.


#### 4. `useCallback`

Memoizes a function itself, not its return value. This is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary re-renders.

```jsx
const handleAddItem = useCallback(() => {
  setItems(prevItems => [...prevItems, 'New Item']);
}, []); // The function instance is stable across re-renders

// Pass handleAddItem to a memoized child component
<MyMemoizedComponent onAddItem={handleAddItem} />
```


#### 5. `useReducer`

An alternative to `useState` for managing more complex state logic or state with multiple sub-values.

* **Analogy:** If `useState` is like having a single light switch, `useReducer` is like a control panel with multiple buttons (`actions`) that can change the lights in more complex ways, all managed by a central logic (`reducer`).

```jsx
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </>
  );
}
```


#### 6. `useEffect` vs `useLayoutEffect`

| Feature | `useEffect` | `useLayoutEffect` |
| :-- | :-- | :-- |
| **Timing** | Runs **asynchronously** after React has rendered and the browser has painted the screen. | Runs **synchronously** after React has performed DOM mutations but **before** the browser has painted. |
| **Use Case** | Most side effects: data fetching, subscriptions. | Reading layout from the DOM and synchronously re-rendering. E.g., measuring an element's size to position a tooltip. |
| **Performance** | Does not block browser painting (better performance). | Blocks browser painting. Can cause performance issues if used incorrectly. |

* **Best Practice:** Always start with `useEffect`. Only switch to `useLayoutEffect` if you experience a visual "flicker" because the DOM was updated before your effect could make a necessary change.

***

Would you like to continue with Section 4: Routing?

---

# yes

Of course. Let's proceed with Section 4.

### Routing in React

In a Single-Page Application (SPA), routing is handled on the client-side. It allows you to change the URL and display different components without causing a full page refresh. **React Router** is the most popular library for this.

#### React Router (v6)

React Router synchronizes the UI of your application with the URL. The latest version (v6) has a more declarative, component-based API.

* **Analogy:** Think of React Router as a traffic controller for your app. The URL is the destination address, and the router directs the "traffic" (the user) to the correct "view" (component) based on that address.


#### Core Components of React Router

| Component | Purpose |
| :-- | :-- |
| **`<BrowserRouter>`** | Wraps your entire application, connecting it to the browser's URL history. It should be used at the root level. |
| **`<Routes>`** | A container for a collection of `<Route>` elements. It intelligently picks the **best match** from its children and renders that component. It replaces the old `<Switch>` component from v5. |
| **`<Route>`** | Declares a mapping between a URL `path` and a React `element`. |
| **`<Link>`** | A component for navigation. It renders an `<a>` tag but prevents a full page reload, instead just changing the URL and letting the router handle the view change. |
| **`<Outlet>`** | Used within a parent route's element to render the matched child route. This is key for **nested layouts**. |

**Basic Routing Example:**

```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="/about" element={<AboutPage />} />
        <Route path="*" element={<NotFoundPage />} /> {/* Catch-all route */}
      </Routes>
    </BrowserRouter>
  );
}
```


***

#### Nested Routes

Nested routes allow you to create layouts where a parent component (like a dashboard with a sidebar) renders a child component based on a more specific URL.

* **Analogy:** This is like a file system. The `/users` route is a folder, and `/users/profile` is a file inside that folder. The `UsersLayout` component is the folder view, and `<Outlet />` is the space where the file's content is displayed.

```jsx
// In your Routes setup
<Route path="/dashboard" element={<DashboardLayout />}>
  <Route path="profile" element={<ProfilePage />} /> {/* Renders at /dashboard/profile */}
  <Route path="settings" element={<SettingsPage />} /> {/* Renders at /dashboard/settings */}
</Route>

// The DashboardLayout component
function DashboardLayout() {
  return (
    <div>
      <Sidebar />
      <main>
        {/* The child route's element will be rendered here */}
        <Outlet />
      </main>
    </div>
  );
}
```


#### Dynamic Routing

Dynamic routes match a pattern in the URL, allowing you to create pages for a variable piece of data, like a user ID or a product slug.

* A colon `:` in the path signifies a dynamic segment.

```jsx
// Route with a dynamic parameter 'userId'
<Route path="/users/:userId" element={<UserProfile />} />

// The UserProfile component, which can access the parameter
import { useParams } from 'react-router-dom';

function UserProfile() {
  // useParams() returns an object of key/value pairs from the URL
  const { userId } = useParams();
  
  // Now you can fetch data for this specific user
  // useEffect(() => fetchUser(userId), [userId]);

  return <h1>Displaying profile for User ID: {userId}</h1>;
}
```


#### Important React Router Hooks

| Hook | Purpose |
| :-- | :-- |
| **`useNavigate()`** | Returns a function that lets you navigate programmatically (e.g., after a form submission). `navigate('/home')`. |
| **`useParams()`** | Returns an object of the dynamic parameters from the current URL. |
| **`useLocation()`** | Returns the current `location` object, which contains info like the `pathname`, `search` (query params), and `state`. |

#### Best Practices \& Common Pitfalls

```
*   **Best Practice:** Always use the `<Link>` component for internal navigation instead of `<a>` tags to leverage client-side routing and prevent page reloads.
```

* **Best Practice:** Define a "catch-all" or "Not Found" route (`path="*"`) at the end of your `<Routes>` configuration to handle invalid URLs gracefully.

```
*   **Common Pitfall (v6):** Forgetting to wrap all your `<Route>` elements inside a `<Routes>` parent. Unlike v5's `<Switch>`, `<Routes>` is mandatory.
```

* **Common Pitfall:** Using `<a>` tags for internal links, which triggers a full page refresh and loses all client-side state.

***

Would you like to continue with Section 5: Forms in React?

---

# yes

Of course. Here are the revision notes for Section 5.

### Forms in React

Handling forms in React involves managing the state of form inputs and handling submission. React offers two main approaches: controlled and uncontrolled components.

#### Controlled vs. Uncontrolled Components

This is a fundamental concept in React forms. The key difference is where the "source of truth" for the form data lives.


| Feature | Controlled Components | Uncontrolled Components |
| :-- | :-- | :-- |
| **Source of Truth** | React state (`useState`). | The DOM itself. |
| **Data Flow** | Value is driven by React state and passed to the input via `value` prop. Changes are handled by `onChange`. | The DOM handles the input's value. You read it imperatively when needed, usually with a `ref`. |
| **Use Case** | Most common. Ideal for forms requiring instant validation, conditional logic, or dynamic inputs. | Simpler forms, integrating with non-React code, or when performance on every keystroke is a major concern. |
| **Implementation** | `useState` to hold the value, updated via `onChange`. | `useRef` to get a reference to the DOM element. |


***

**Controlled Component: The React Way**

Here, the component's state is the single source of truth. Every keystroke triggers a re-render.

* **Analogy:** A controlled component is like a puppet. The React state is the puppeteer, pulling the strings (`value` prop) to control the puppet's exact position. The `onChange` handler reports back any attempts by the outside world to move the puppet.

```jsx
function ControlledForm() {
  const [name, setName] = useState('');

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`A name was submitted: ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input 
          type="text" 
          value={name} // State drives the input value
          onChange={(e) => setName(e.target.value)} // State is updated on change
        />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}
```

* **Best Practice:** This is the recommended approach for most forms in React as it makes validation and state management explicit.

***

**Uncontrolled Component: The Traditional HTML Way**

Here, the form data is handled by the DOM itself. You pull the value from the DOM when you need it.

* **Analogy:** An uncontrolled component is like setting a wind-up toy and letting it go. You don't manage its every move; you just check its final position (`ref.current.value`) when it stops.

```jsx
function UncontrolledForm() {
  const inputRef = useRef(null);

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`A name was submitted: ${inputRef.current.value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        {/* No value prop. The DOM manages its own state. */}
        <input type="text" ref={inputRef} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}
```


***

#### Form Libraries

For complex forms with validation, error handling, and submission logic, using a dedicated library is highly recommended. They solve common problems efficiently.


| Library | Key Idea | Performance |
| :-- | :-- | :-- |
| **Formik** | A comprehensive solution that manages form state, validation, and submission handlers. It was the long-time standard but is less popular now. | Good, but can cause re-renders on the parent component holding the form state. |
| **React Hook Form** | A minimal, hook-based library focused on performance. It uses refs (uncontrolled approach) to minimize re-renders. | **Excellent**. It isolates re-renders to only the inputs that need to change, not the entire form component. |

**React Hook Form Example:**

This library is loved for its simplicity and performance.

```jsx
import { useForm } from 'react-hook-form';

function MyForm() {
  const { register, handleSubmit, formState: { errors } } = useForm();
  
  const onSubmit = (data) => console.log(data);

  return (
    // handleSubmit will validate your inputs before invoking "onSubmit"
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* "register" links the input to the form state and validation rules */}
      <input defaultValue="test" {...register("firstName", { required: true })} />
      {/* errors will return when field validation fails  */}
      {errors.firstName && <span>This field is required</span>}
      
      <input type="submit" />
    </form>
  );
}
```


#### Best Practices \& Common Pitfalls

* **Pitfall (Controlled):** Performance issues in large forms. Because the component re-renders on every keystroke, it can become slow. This is the main problem **React Hook Form** solves.
* **Pitfall (General):** Forgetting the `name` attribute on inputs. This is essential for both libraries and for handling multiple fields in a single state object.
* **Best Practice:** Always provide clear and immediate validation feedback to the user. Display errors next to the relevant fields.
* **Best Practice:** Disable the submit button while the form is submitting to prevent duplicate submissions.

***

Would you like to continue with Section 6: React Rendering and Reconciliation?

---

# yes

Of course. Let's cover Section 6.

### React Rendering and Reconciliation

This section explains how React updates the UI efficiently. Understanding this process is key to writing performant React applications.

#### What is Rendering?

In React, **rendering** is the process of calling a component's function (or `render` method in classes) to determine what should appear on the screen. This doesn't mean the DOM is updated yet. The output is a tree of React elements, often called the **Virtual DOM**.

**A component re-renders if:**

* Its **state** changes (via `useState` or `useReducer`).
* Its **props** change.
* Its **parent component** re-renders.
* A **context** it subscribes to provides a new value.

***

#### What is Reconciliation?

**Reconciliation** is the process React uses to update the actual DOM to match the latest render output. After a component re-renders, React has two Virtual DOM trees: the old one and the new one. The process of comparing these two trees to find the differences is called the **diffing algorithm**.

* **Analogy:** Imagine you're a copy editor with two versions of a long document. Instead of rewriting the entire document from scratch (rebuilding the DOM), you carefully compare them line by line (`diffing`) and only mark the specific words and sentences that have changed. This is much faster. React does this with your UI tree.


#### The Diffing Algorithm

React's diffing algorithm uses heuristics to achieve a fast comparison.

```
1.  **Different Element Types:** If the root elements of the two trees have different types (e.g., an `<h1>` is replaced by a `<p>`), React will **tear down the old tree completely** and build the new tree from scratch. This includes unmounting all old components and mounting new ones, which means their state is lost.
```

2. **Same Element Types:** If the root elements are of the same type (e.g., both are `<div>`), React keeps the same underlying DOM node and only updates the attributes (`className`, `style`, etc.) that have changed. It then moves on to recursively compare the children of these nodes.
3. **Lists of Elements and the `key` Prop:** When comparing a list of children, React by default will compare them based on their order. This can be very inefficient for lists where items are added, removed, or reordered.

This is where the **`key`** prop becomes essential.

#### The `key` Prop: A Hint for React

A `key` is a special string attribute you need to include when creating lists of elements. Keys help React identify which items have changed, been added, or been removed.

* **Analogy:** Think of children lining up. If a child leaves, you wouldn't assume everyone after them is a new person. You would identify them by their **name (`key`)**. If "Charlie" leaves the line, you know it's "Charlie" who is gone, and "David" and "Eve" just moved up one spot. Without names, you might think "Charlie" just changed into "David," "David" into "Eve," and so on, which is confusing and wrong.

**Why are keys important?**

* **Performance:** They allow React to avoid re-rendering or mutating an element if it just moved. It can find the element with the same key and just move it.
* **State Preservation:** Keys ensure that the internal state of a component (like the text inside an `<input>`) is preserved correctly when the list is reordered.

```jsx
// Good: Using a stable, unique ID as a key
<ul>
  {todos.map(todo => (
    <li key={todo.id}>{todo.text}</li>
  ))}
</ul>

// Bad: Using the array index as a key
<ul>
  {todos.map((todo, index) => (
    <li key={index}>{todo.text}</li>
  ))}
</ul>
```

* **Common Pitfall:** Using the array `index` as a `key`. This is a major anti-pattern for dynamic lists. If an item is added to the beginning of the list, all indices shift. React will think every list item has new props and may update them incorrectly, leading to bugs and performance issues. Only use `index` as a key if the list is **static and will never change**.
* **Best Practice:** The best `key` is a string that is **unique** among its siblings and **stable** (it doesn't change across re-renders). This is usually a unique ID from your data (e.g., `user.id`, `product.uuid`).

***

Would you like to continue with Section 7: Performance Optimization?

---

# yes

Of course. Let's move on to Section 7.

### Performance Optimization

Performance optimization in React focuses on making your application faster by reducing its initial load time and ensuring smooth UI interactions. The primary goals are to prevent unnecessary re-renders and to load code only when it's needed.

**Best Practice:** Don't optimize prematurely. Use the **React DevTools Profiler** to identify performance bottlenecks first, then apply these techniques where they are most needed.

***

#### 1. Memoization

Memoization is a form of caching. You store the results of expensive operations and return the cached result when the same inputs occur again.

* **Analogy:** Imagine a chef being asked to bake a complex cake. The first time, it takes hours. If asked for the exact same cake again, a "memoized" chef would simply serve a slice from the one they already baked, saving time and effort.

There are three main tools for memoization in React:


| Tool | What It Memoizes | When to Use |
| :-- | :-- | :-- |
| **`React.memo()`** | An entire **component**. | Wrap a component to prevent it from re-rendering if its `props` have not changed. It performs a shallow comparison of props. |
| **`useMemo()`** | The **return value** of a function. | To avoid re-calculating the result of an expensive function on every render. |
| **`useCallback()`** | A **function definition** itself. | To prevent a function from being recreated on every render. Crucial when passing callbacks to memoized child components. |

**`React.memo()` Example:**

```jsx
const UserAvatar = React.memo(function UserAvatar({ userName }) {
  // This component will only re-render if the 'userName' prop changes.
  // It will NOT re-render if its parent re-renders for other reasons.
  console.log(`Rendering avatar for ${userName}`);
  return <img src={`/avatars/${userName}`} alt={userName} />;
});

// Parent component
function ProfilePage({ user, theme }) {
  // Even if 'theme' changes and ProfilePage re-renders, UserAvatar will not.
  return (
    <div>
      <UserAvatar userName={user.name} />
      <p>Current theme: {theme}</p>
    </div>
  );
}
```

* **Common Pitfall:** Wrapping a component in `React.memo` but passing a new function (`onClick={() => {}}`) as a prop on every render. This defeats the purpose of memoization because the function is a new object every time. This is exactly what `useCallback` is for.

***

#### 2. Code Splitting and Lazy Loading

Code splitting breaks your app's JavaScript bundle into smaller chunks that can be loaded on demand, rather than all at once. This dramatically improves initial load time.

* **`React.lazy()`**: A function that lets you render a dynamic `import()` as a regular component.
* **`<Suspense>`**: A component that lets you specify a loading indicator (a "fallback" UI) if the component you're trying to render is not yet loaded.

```jsx
import React, { Suspense, useState } from 'react';

// This component will be loaded in a separate chunk.
const AdminDashboard = React.lazy(() => import('./components/AdminDashboard'));

function App() {
  const [showAdmin, setShowAdmin] = useState(false);

  return (
    <div>
      <h1>My App</h1>
      <button onClick={() => setShowAdmin(true)}>Load Admin Panel</button>
      
      {/* Show a loading message while the AdminDashboard component is being fetched */}
      <Suspense fallback={<div>Loading...</div>}>
        {showAdmin && <AdminDashboard />}
      </Suspense>
    </div>
  );
}
```

* **Best Practice:** Use code splitting for route-based components (e.g., loading a page's code only when the user navigates to it) or for large components that are not needed on the initial page load (e.g., a complex modal).

***

#### 3. Virtualization (or "Windowing")

This technique is for rendering long lists of data efficiently. Instead of rendering all items in a list (which could be thousands of DOM nodes), you only render the small subset of items currently visible in the viewport.

* **Analogy:** Instead of printing an entire 10,000-page dictionary, you use a digital version that only shows the 20-30 entries visible on your screen at any time. As you scroll, it quickly replaces the old entries with new ones.
* This is not a built-in React feature. You need to use libraries like **`react-window`** or **`react-virtualized`**.


#### 4. React 18+ Performance Features

* **Automatic Batching:** React 18 automatically batches multiple state updates into a single re-render, even those inside promises, timeouts, or native event handlers. This reduces unnecessary renders out-of-the-box.
* **Transitions (`useTransition`)**: A new concurrency feature that lets you mark certain state updates as non-urgent ("transitions"). This allows React to prioritize important updates (like user input) and keep the UI responsive, even during heavy rendering tasks.

```jsx
const [isPending, startTransition] = useTransition();

// An urgent update
setInputValue(e.target.value);

// A non-urgent update wrapped in a transition
startTransition(() => {
  setSearchQuery(e.target.value); // This update can be interrupted
});
```


***

Would you like to continue with Section 8: Advanced Patterns?

---

# yes

Of course. Here are the revision notes for Section 8.

### Advanced Patterns

These patterns provide powerful and flexible ways to reuse component logic and create highly composable UIs. While hooks have replaced some of their use cases, they are still important to understand, especially in existing codebases.

***

#### 1. Higher-Order Components (HOCs)

A Higher-Order Component is a **function** that takes a component and returns a new component with additional props or logic.

* **Core Idea:** `const EnhancedComponent = withSomething(WrappedComponent);`
* **Analogy:** An HOC is like a decorator for a component. If you have a plain cake (`WrappedComponent`), an HOC (`withSprinkles`) can take that cake and return a new one that looks the same but now has sprinkles on top (additional `props` or behavior).
* **Use Cases:**
    * Injecting props (e.g., `withRouter` from old React Router).
    * Managing side effects (e.g., connecting to a Redux store with `connect`).
    * Abstracting away common logic (e.g., `withAuth` to protect a route).

**Example: `withLogger` HOC**

This HOC logs a component's props whenever it renders.

```jsx
// This is the HOC function
function withLogger(WrappedComponent) {
  // It returns a new component...
  return function EnhancedComponent(props) {
    useEffect(() => {
      console.log(`Component ${WrappedComponent.name} rendered with props:`, props);
    });

    // ...that renders the original component with the original props
    return <WrappedComponent {...props} />;
  };
}

// A simple component to wrap
function MyComponent({ message }) {
  return <div>{message}</div>;
}

// Create the enhanced component
const MyComponentWithLogger = withLogger(MyComponent);

// Usage
<MyComponentWithLogger message="Hello" />
```

* **Common Pitfalls:**
    * **Prop name collisions:** The HOC might inject a prop name that is already used by the wrapped component.
    * **"Wrapper hell":** Chaining many HOCs can lead to deeply nested component trees in the React DevTools, making debugging difficult (`withRouter(withRedux(withTheme(MyComponent)))`).

***

#### 2. Render Props

A component with a **render prop** is a component that takes a function as one of its props (conventionally named `render`) and calls that function to determine what to render.

* **Core Idea:** The component manages some state or logic but lets the parent decide **what** to render with that state. It inverts control.
* **Analogy:** A render prop component is like a vending machine (`<DataProvider>`). It has access to internal data (the snacks). You tell it what you want by providing instructions (`render` prop): "When you have the data, give me a component that displays it in a blue box." The vending machine handles getting the data; you just define the presentation.

**Example: `MouseTracker`**

This component tracks the mouse position but lets its parent decide how to render it.

```jsx
class MouseTracker extends React.Component {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  const handleMouseMove = (event) => {
    setPosition({ x: event.clientX, y: event.clientY });
  };

  return (
    <div style={{ height: '100vh' }} onMouseMove={handleMouseMove}>
      {/* Call the render prop with the current state */}
      {this.props.render(position)}
    </div>
  );
}

// Usage
function App() {
  return (
    <div>
      <h1>Move the mouse around!</h1>
      <MouseTracker render={mouse => (
        <p>The mouse position is {mouse.x}, {mouse.y}</p>
      )}/>
    </div>
  );
}
```

* **React Version Note:** Today, this pattern is almost entirely replaced by **custom hooks**. A `useMousePosition()` hook would provide the same logic far more simply without the nesting.

***

#### 3. Custom Hooks

A custom hook is a JavaScript function whose name starts with "**`use`**" and that calls other hooks. This is the modern, recommended way to reuse stateful logic between components.

* **Core Idea:** Extract component logic into reusable functions.
* **Benefits over HOCs and Render Props:**
    * No extra components in the tree (avoids "wrapper hell").
    * More explicit and easier to follow where the logic comes from.
    * Can return multiple values, giving the consuming component full control.

**Example: `useMousePosition` (replacing the render prop example)**

```jsx
// The custom hook
function useMousePosition() {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  useEffect(() => {
    const handleMouseMove = (event) => {
      setPosition({ x: event.clientX, y: event.clientY });
    };

    window.addEventListener('mousemove', handleMouseMove);

    return () => {
      window.removeEventListener('mousemove', handleMouseMove);
    };
  }, []); // Empty array ensures this effect runs only once

  return position;
}

// Usage in any component
function MyComponent() {
  const position = useMousePosition(); // Clean and direct
  return <p>The mouse is at {position.x}, {position.y}</p>;
}
```


#### 4. Compound Components

This pattern involves a set of components that work together to manage a shared state and perform a common task. The parent component implicitly manages the state for its children.

```
*   **Analogy:** A `<select>` and `<option>` element in HTML. The `<select>` manages which option is selected, but the `<option>` elements define the individual choices. They are useless on their own but powerful together.
```

* **Implementation:** Usually achieved with **Context API**. The parent is the `Context.Provider`, and the children use `useContext` to access the shared state and functions.

**Example: A Custom `Tabs` Component**

```jsx
// Using Context to create a compound component
const TabsContext = React.createContext();

function Tabs({ children }) {
  const [activeTab, setActiveTab] = useState(children[0].props.label);
  return (
    <TabsContext.Provider value={{ activeTab, setActiveTab }}>
      {children}
    </TabsContext.Provider>
  );
}

function Tab({ label, children }) {
  const { activeTab, setActiveTab } = useContext(TabsContext);
  const isActive = activeTab === label;
  
  return (
    <div>
      <button onClick={() => setActiveTab(label)}>{label}</button>
      {isActive && <div>{children}</div>}
    </div>
  );
}

// Usage
<Tabs>
  <Tab label="Tab 1">Content for Tab 1</Tab>
  <Tab label="Tab 2">Content for Tab 2</Tab>
</Tabs>
```


***

Would you like to continue with Section 9: Portals \& Error Boundaries?

---

# yes

Of course. Here is the quick revision guide for Section 9.

### Portals \& Error Boundaries

These are two specialized but powerful features in React for handling UI that needs to "escape" its component hierarchy or for gracefully managing runtime errors.

***

### Portals

A portal provides a first-class way to render children into a DOM node that exists **outside the parent component's DOM hierarchy**.

* **Core Idea:** The component lives in one place in the React tree, but its rendered output appears somewhere else in the DOM.
* **Analogy:** Imagine a video game character finding a magical portal. They can step through it and instantly appear in a completely different part of the map. In React, a portal lets your component's visuals "teleport" to another part of the DOM, like `document.body`.
* **Why use portals?**
The most common use case is for UI elements that need to break out of their containers to avoid CSS issues like `overflow: hidden` or `z-index` stacking problems.
    * **Modals and Dialogs:** A modal should cover the entire screen, but if it's rendered inside a container with `overflow: hidden`, it will be clipped. A portal renders it directly into `document.body`.
    * **Tooltips and Popovers:** These often need to be positioned relative to the viewport, not their parent element.
    * **Notifications:** Global notifications that appear at the top or bottom of the screen.

**How it works:**

You use the `createPortal` function from `react-dom`.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

// A modal component using a portal
function Modal({ children }) {
  // The first argument is the JSX you want to render.
  // The second argument is the DOM element to render it into.
  return ReactDOM.createPortal(
    <div className="modal-backdrop">
      <div className="modal-content">{children}</div>
    </div>,
    document.getElementById('modal-root') // Assumes you have <div id="modal-root"></div> in your public/index.html
  );
}

// Usage
function App() {
  const [showModal, setShowModal] = useState(false);

  return (
    <div>
      <button onClick={() => setShowModal(true)}>Show Modal</button>
      {showModal && (
        <Modal>
          <h2>This is a Modal</h2>
          <p>It's rendered outside the main app div!</p>
          <button onClick={() => setShowModal(false)}>Close</button>
        </Modal>
      )}
    </div>
  );
}
```

* **Important Note:** Even though a portal renders its DOM nodes elsewhere, it still behaves like a normal React child within the component tree. This means it can access **context** provided by its ancestors and **events will bubble up** to its ancestors in the React tree, not the DOM tree.

***

### Error Boundaries

An Error Boundary is a special class component that can **catch JavaScript errors** anywhere in its child component tree, log those errors, and display a **fallback UI** instead of letting the entire component tree crash.

* **Analogy:** An error boundary is like a circuit breaker in your house's electrical system. If one appliance short-circuits (a component throws an error), the circuit breaker trips and contains the problem to that one circuit, preventing the whole house from losing power (the entire app crashing).
* **Key Features:**
    * They are implemented as **class components**. There is no hook equivalent for error boundaries yet.
    * They must define at least one of two special lifecycle methods:
        * `static getDerivedStateFromError(error)`: Used to update state so the next render will show the fallback UI.
        * `componentDidCatch(error, errorInfo)`: Used for side effects like logging the error to an external service (e.g., Sentry, LogRocket).

**How to create an Error Boundary:**

```jsx
import React from 'react';

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  // This lifecycle is triggered after a descendant component throws an error.
  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  // This lifecycle is also triggered, and is good for logging errors.
  componentDidCatch(error, errorInfo) {
    console.error("Uncaught error:", error, errorInfo);
    // logErrorToMyService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI.
      return <h1>Something went wrong. Please refresh the page.</h1>;
    }

    // If there's no error, just render the children.
    return this.props.children;
  }
}
```

**How to use it:**

You wrap it around parts of your application that might fail.

```jsx
<ErrorBoundary>
  <MyProfileWidget />
</ErrorBoundary>
<ErrorBoundary>
  <AnotherWidget />
</ErrorBoundary>
```

* **Best Practice:** Don't wrap your entire app in a single error boundary. Place them strategically around independent parts of your UI (widgets, routes, sidebars) so that a failure in one part doesn't take down the entire page.
* **Error boundaries do NOT catch errors from:**
    * Event handlers (use a standard `try...catch` block inside them).
    * Asynchronous code (`setTimeout`, promises).
    * Server-side rendering.
    * Errors thrown in the error boundary itself.

***

Would you like to continue with Section 10: Refs and DOM Manipulation?

---

# yes

Of course. Here is the revision guide for Section 10.

### Refs and DOM Manipulation

While React's declarative nature means you usually don't need to touch the DOM directly, sometimes you need to "break the glass" and access a DOM element or a class component instance imperatively. Refs are the tool for this job.

#### What is a Ref?

A ref is an object with a single `current` property. It's like a box that can hold a value. Unlike state, updating a ref does **not** trigger a re-render.

* **Analogy:** A `ref` is like a direct phone line to a specific DOM element. Instead of sending messages through the usual React channels (props and state), you can pick up the phone and give a direct command, like "focus now!"

There are two main use cases for refs:

1. **Accessing DOM nodes:** To manage focus, trigger animations, or integrate with third-party DOM libraries.
2. **Storing a mutable value:** To keep track of a value across renders without causing a re-render (e.g., a timer ID).

***

#### 1. `useRef`

The `useRef` hook is the standard way to create refs in functional components.

**Use Case 1: Accessing a DOM Element**

```jsx
import React, { useRef, useEffect } from 'react';

function TextInputWithFocusButton() {
  // 1. Create the ref
  const inputEl = useRef(null);

  const onButtonClick = () => {
    // 3. Access the DOM node via inputEl.current
    inputEl.current.focus();
  };

  return (
    <>
      {/* 2. Attach the ref to the DOM element */}
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

* **Best Practice:** Only access `ref.current` inside `useEffect` or event handlers. During the initial render, `ref.current` will be `null` because the DOM node hasn't been created yet.

**Use Case 2: Storing a Mutable Value**

This is useful for storing information that shouldn't trigger a re-render.

```jsx
function Timer() {
  const intervalRef = useRef(null);
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Store the interval ID in the ref
    intervalRef.current = setInterval(() => {
      setCount(c => c + 1);
    }, 1000);

    // Clean up on unmount
    return () => clearInterval(intervalRef.current);
  }, []);

  return <h1>{count}</h1>;
}
```


***

#### 2. `forwardRef`

By default, functional components cannot be given a `ref`. If you try to put a `ref` on a custom component (`<MyInput ref={myRef} />`), it won't work.

`forwardRef` lets a component receive a `ref` and "forward" it down to one of its children (usually a DOM element).

* **Analogy:** `forwardRef` is like a mail forwarding service. A letter (`ref`) arrives addressed to your component's house, but you have instructions to immediately pass it along to the person living in the basement (the `input` element).

**Example:**

Let's make our `TextInputWithFocusButton` reusable.

```jsx
// Create a component that can be focused from the outside
const FancyInput = React.forwardRef((props, ref) => {
  return (
    <div>
      <label>{props.label}</label>
      {/* Forward the incoming ref to the input element */}
      <input ref={ref} {...props} />
    </div>
  );
});

// Parent component using the FancyInput
function App() {
  const fancyInputRef = useRef(null);

  const handleClick = () => {
    fancyInputRef.current.focus();
  };

  return (
    <>
      <FancyInput ref={fancyInputRef} label="My Fancy Input" />
      <button onClick={handleClick}>Focus Fancy Input</button>
    </>
  );
}
```


***

#### 3. `useImperativeHandle`

This hook is a more advanced tool that customizes the value that is exposed to parent components when they use `ref`. Instead of forwarding the entire DOM node, you can expose a smaller, custom "handle" with specific functions.

* **Core Idea:** You are defining a public API for your component that can be accessed via a ref.
* **Best Practice:** This should be used sparingly. Imperative code is harder to reason about than declarative code. It's an escape hatch for when you truly need it.

**Example:**

Let's create a `FancyInput` that can be focused and also have its value cleared imperatively.

```jsx
import { forwardRef, useRef, useImperativeHandle } from 'react';

const FancyInputWithHandle = forwardRef((props, ref) => {
  const inputRef = useRef();
  
  // Expose a custom handle with specific methods
  useImperativeHandle(ref, () => ({
    // The parent can call ref.current.focusInput()
    focusInput: () => {
      inputRef.current.focus();
    },
    // The parent can call ref.current.clearInput()
    clearInput: () => {
      inputRef.current.value = '';
    }
  }));

  return <input ref={inputRef} />;
});

// Usage
function App() {
  const fancyRef = useRef(null);

  return (
    <>
      <FancyInputWithHandle ref={fancyRef} />
      <button onClick={() => fancyRef.current.focusInput()}>Focus</button>
      <button onClick={() => fancyRef.current.clearInput()}>Clear</button>
    </>
  );
}
```

* **Common Pitfall:** Over-exposing imperative methods. Try to solve problems with props and state first. `useImperativeHandle` is for cases where props are not sufficient, such as triggering a non-declarative animation or managing focus.

***

Would you like to continue with Section 11: React with TypeScript?

---

# yes

Here are quick revision notes for Section 11: React with TypeScript.

***

### React with TypeScript

Strong typing in React projects improves maintainability and reduces bugs—crucial for interview settings and scaling codebases.

#### 1. Props Typing

You can type props using either **interfaces** or **type aliases**. Both work, but interfaces are more extensible for libraries, while types are more common for props and states in apps.

```tsx
// Using interface
interface ButtonProps {
  label: string;
  disabled?: boolean;
  onClick: () => void;
}

const Button: React.FC<ButtonProps> = ({ label, disabled, onClick }) => (
  <button disabled={disabled} onClick={onClick}>
    {label}
  </button>
);

// Using type alias (equivalent)
type ButtonPropsType = {
  label: string;
  disabled?: boolean;
  onClick: () => void;
};
```

**Best Practice:** For extended components or libraries, stick to `interface`; for simple prop composition and unions, use `type`.

***

#### 2. Typing Children

- By default, TypeScript does **not** include `children` in custom prop interfaces.
- Use `PropsWithChildren<YourProps>` or extend with `children?: React.ReactNode`.

```tsx
import { PropsWithChildren } from "react";

interface CardProps {
  title: string;
}
const Card = (props: PropsWithChildren<CardProps>) => (
  <div>
    <h2>{props.title}</h2>
    {props.children}
  </div>
);
```

*Common Pitfall:* Forgetting to type `children` if your component relies on it, leading to TS errors.

***

#### 3. Typing Hooks

- **useState**: Inferred from initial value for primitives, explicit for complex types or when starting with `null`.

```tsx
const [count, setCount] = useState(0); // inferred as number
const [user, setUser] = useState<User | null>(null); // explicit as User | null
```

- **useReducer**: Use discriminated unions for actions and type the state up front.

```tsx
type Action =
  | { type: "increment"; value: number }
  | { type: "decrement"; value: number };

const reducer = (state: number, action: Action): number => {
  switch (action.type) {
    case "increment": return state + action.value;
    case "decrement": return state - action.value;
    default: return state;
  }
};

const [state, dispatch] = useReducer(reducer, 0);
```

- **useRef**: Always add types for DOM elements like `HTMLInputElement`.

```tsx
const inputRef = useRef<HTMLInputElement>(null);
```

*Common Pitfall:* Using `useRef(null)` without the explicit type—loses type safety.

***

#### 4. Generics in Components and Hooks

Generics allow you to create reusable and type-safe components and hooks.

```tsx
// Generic component example
interface ListProps<T> {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
}

function List<T>({ items, renderItem }: ListProps<T>) {
  return <ul>{items.map(renderItem)}</ul>;
}
```

*Common Pitfall:* Forgetting to annotate the generic parameter in arrow functions:

```tsx
const List = <T,>({ items, renderItem }: ListProps<T>) => ...
```


***

#### 5. Utility Types

TypeScript offers powerful built-in utility types, commonly used in React projects:


| Utility Type | Purpose | Example Usage |
| :-- | :-- | :-- |
| `Partial<T>` | All properties are optional | `Partial<User>` |
| `Required<T>` | All properties become required | `Required<User>` |
| `Pick<T, K>` | Select only `K` keys from `T` | `Pick<User, "id"|"name">` |
| `Omit<T, K>` | Exclude `K` keys from `T` | `Omit<User, "password">` |
| `Record<K, T>` | Object with keys of type `K` and values of type `T` | `Record<string, number>` |

*Interview Tip:* Be ready to "map" props using these types for pattern questions or when composing component APIs.

***

#### 6. Typing Event Handlers

Use React's built-in event types for typing form controls and DOM events.

```tsx
const handleInput = (e: React.ChangeEvent<HTMLInputElement>) => {
  console.log(e.target.value);
};
```


***

#### 7. Typing Custom Hooks

To avoid union arrays, use tuple assertions when returning arrays from hooks.

```tsx
export function useCounter() {
  const [count, setCount] = useState(0);
  const increment = () => setCount(c => c + 1);
  return [count, increment] as const; // [number, () => void]
}
```


***

#### React Version Notes (18+ and 19)

- Types for hooks are well-supported since v16.8.
- `React.FC` became less recommended for new projects—prefer direct typing of props and explicit typing for `children`.
- Utility types (`PropsWithChildren`, `ComponentProps`, etc.) are refined for strictness and compatibility with concurrent features.

***

#### Common Interview Pitfalls

- Failing to annotate generic arrow function components with a trailing comma (`<T,>`).
- Not specifying types for hooks whose initial state is `null` or an empty object.
- Forgetting to add types to custom hooks’ return values, causing implicit `any` types.

***

Would you like to continue with Section 12: React with Backend APIs?
<span style="display:none">[^12_1][^12_10][^12_11][^12_12][^12_13][^12_14][^12_15][^12_16][^12_17][^12_18][^12_19][^12_2][^12_20][^12_3][^12_4][^12_5][^12_6][^12_7][^12_8][^12_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^12_1]: https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example/

[^12_2]: https://react.dev/learn/typescript

[^12_3]: https://dev.to/typescripttv/typing-react-props-in-typescript-5hal

[^12_4]: https://www.totaltypescript.com/react-props-typescript

[^12_5]: https://blog.bitsrc.io/react-with-typescript-cheatsheet-9dd891dc5bfe

[^12_6]: https://stackoverflow.com/questions/53650468/set-types-on-usestate-react-hook-with-typescript

[^12_7]: https://www.freecodecamp.org/news/typescript-generics-with-functional-react-components/

[^12_8]: https://dev.to/rajatkaush1k/12-must-have-typescript-utility-types-with-uses-and-examples-213j

[^12_9]: https://stackoverflow.com/questions/43230765/typescript-react-access-component-property-types

[^12_10]: https://dev.to/mbarzeev/converting-your-react-hook-to-typescript-380e

[^12_11]: https://www.totaltypescript.com/tips/use-generics-in-react-to-make-dynamic-and-flexible-components

[^12_12]: https://www.typescriptlang.org/docs/handbook/utility-types.html

[^12_13]: https://meje.dev/blog/type-checking-in-typescript

[^12_14]: https://devtrium.com/posts/react-typescript-how-to-type-hooks

[^12_15]: https://www.developerway.com/posts/typescript-generics-for-react-developers

[^12_16]: https://www.w3schools.com/typescript/typescript_utility_types.php

[^12_17]: https://www.reddit.com/r/reactjs/comments/152zs2q/typescript_react_best_way_to_define_component/

[^12_18]: https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks/

[^12_19]: https://www.typescriptlang.org/docs/handbook/2/generics.html

[^12_20]: https://react-typescript-cheatsheet.netlify.app/docs/advanced/utility_types/


---

# yes

Of course. Here is the revision guide for Section 12.

### React with Backend APIs

Connecting to a backend is a core task for most React applications. This involves fetching data, handling loading and error states, and sending data back to the server. Modern React has shifted from manual fetching to powerful data-synchronization libraries.

#### 1. Traditional Method: `useEffect` + `useState`

The original approach involved using `useEffect` to trigger a fetch request and `useState` to manage the various states of the request.

```jsx
import { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchUser = async () => {
      try {
        setLoading(true);
        const response = await fetch(`https://api.example.com/users/${userId}`);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await response.json();
        setUser(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchUser();
  }, [userId]); // Re-fetch if userId changes

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;

  return <div><h1>{user?.name}</h1></div>;
}
```

* **React Version Note:** While this pattern works, it's now considered a **low-level approach**. It is verbose and requires you to manually handle caching, race conditions, and re-fetching, which is complex and error-prone. Modern best practice is to use a dedicated library.[^13_1][^13_2]

***

#### 2. HTTP Clients: `fetch` vs. `axios`

You can use the native `fetch` API or a library like `axios` to make HTTP requests.


| Feature | `fetch` (Native Browser API) | `axios` (Third-party Library) |
| :-- | :-- | :-- |
| **JSON Parsing** | Manual: requires an extra `.json()` step on the response body[^13_3]. | Automatic: response data is already parsed as JSON[^13_4]. |
| **Error Handling** | Doesn't reject on HTTP error statuses (like 404 or 500). You must check `response.ok` manually[^13_3]. | Rejects the promise on network errors and HTTP error statuses, making `catch` blocks more reliable[^13_4]. |
| **Interceptors** | Not supported natively. | Supported: allows you to intercept requests and responses to transform data or add headers (e.g., auth tokens) globally[^13_4][^13_3]. |
| **Setup** | Built-in, no installation needed[^13_5]. | Requires installation (`npm install axios`). |
| **Browser Support** | Modern browsers only (no IE)[^13_4]. | Wide browser support[^13_3]. |

* **Best Practice:** For simple GET requests, `fetch` is fine. For applications with more complex needs like global error handling or authentication, `axios` provides more power out-of-the-box.

***

#### 3. Modern Data-Fetching Libraries: The "Server State" Solution

Libraries like **React Query (now TanStack Query)** and **SWR** are the modern standard. They treat backend data as **server state**, which is different from client state because it's stored remotely and can be changed by others. These libraries handle caching, re-fetching, and synchronization automatically.


| Library | Key Concept |
| :-- | :-- |
| **React Query** | A powerful library that manages server state with features like caching, background re-fetching, devtools, pagination, and mutations[^13_6]. |
| **SWR** | A lightweight library based on the `stale-while-revalidate` caching strategy. It serves stale data from the cache first (for a fast UI), then re-fetches in the background and updates the view[^13_7][^13_8]. |

**React Query Example:**

```jsx
import { useQuery } from '@tanstack/react-query';
import axios from 'axios';

const fetchUser = async (userId) => {
  const { data } = await axios.get(`https://api.example.com/users/${userId}`);
  return data;
};

function UserProfile({ userId }) {
  // useQuery handles all the loading, error, and data states for you
  const { data: user, isLoading, isError, error } = useQuery({
    queryKey: ['user', userId], // A unique key for this query
    queryFn: () => fetchUser(userId),
  });

  if (isLoading) return <div>Loading...</div>;
  if (isError) return <div>Error: {error.message}</div>;

  return <div><h1>{user.name}</h1></div>;
}
```

* **Why is this better?** It automatically handles caching, re-fetching data when you re-focus the window, and provides hooks like `useMutation` for easy data updates (POST, PUT, DELETE).

***

#### 4. GraphQL Integration: Apollo Client

If your backend uses GraphQL, **Apollo Client** is the go-to solution. It provides a similar set of hooks to React Query but is specifically tailored for GraphQL's query language.

```jsx
import { gql, useQuery } from '@apollo/client';

// Define the GraphQL query
const GET_USER = gql`
  query GetUser($userId: ID!) {
    user(id: $userId) {
      id
      name
      email
    }
  }
`;

function UserProfile({ userId }) {
  const { loading, error, data } = useQuery(GET_USER, {
    variables: { userId },
  });

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return <div><h1>{data.user.name}</h1></div>;
}
```

* **Benefit:** Apollo Client integrates deeply with GraphQL, providing automatic cache updates after mutations and a rich set of tools for managing a GraphQL-based application.[^13_9][^13_10]

***

Would you like to continue with Section 13: Styling in React?
<span style="display:none">[^13_11][^13_12][^13_13][^13_14][^13_15][^13_16][^13_17][^13_18][^13_19][^13_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^13_1]: https://www.reddit.com/r/reactjs/comments/15yz949/how_to_actually_fetch_data_in_react/

[^13_2]: https://www.creolestudios.com/react-data-fetching-best-practices/

[^13_3]: https://www.geeksforgeeks.org/node-js/difference-between-fetch-and-axios-js-for-making-http-requests/

[^13_4]: https://apidog.com/articles/react-fetch-vs-axios/

[^13_5]: https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch

[^13_6]: https://tanstack.com/query/v3/docs/react/overview

[^13_7]: https://swr.vercel.app

[^13_8]: https://github.com/vercel/swr

[^13_9]: https://www.geeksforgeeks.org/mern/how-to-integrate-graphql-in-react-js/

[^13_10]: https://www.apollographql.com/docs/react

[^13_11]: https://www.youtube.com/watch?v=MBlZ8Wzkbi4

[^13_12]: https://reacttraining.com/blog/modern-data-fetching-in-react

[^13_13]: https://blog.logrocket.com/modern-api-data-fetching-methods-react/

[^13_14]: https://nextjs.org/docs/14/app/building-your-application/data-fetching/patterns

[^13_15]: https://dev.to/otamnitram/react-query-a-practical-example-167j

[^13_16]: https://refine.dev/blog/react-query-guide/

[^13_17]: https://refine.dev/blog/data-fetching-next-js-useswr/

[^13_18]: https://www.youtube.com/watch?v=iO6px_wz1oc

[^13_19]: https://blog.logrocket.com/axios-vs-fetch-2025/

[^13_20]: https://dev.to/debajit13/getting-started-with-graphql-and-react-b5k


---

# yes

Of course. Let's proceed with Section 13.

### Styling in React

Styling is a critical part of building a React application. There are several popular approaches, each with its own trade-offs regarding scope, maintainability, and developer experience.

***

#### 1. CSS Modules

CSS Modules are CSS files where all class names are **scoped locally** by default. This solves the classic CSS problem of global scope and class name collisions.[^14_1]

* **How it works:** You name your stylesheet `[ComponentName].module.css`. When you import it into your component, the build process generates unique class names for you.[^14_2][^14_1]

```jsx
/* Button.module.css */
.button {
  background-color: steelblue;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}
```

```jsx
// Button.js
import React from 'react';
import styles from './Button.module.css'; // Import the module

function Button() {
  // Use the imported 'styles' object to apply the class
  return <button className={styles.button}>Click Me</button>;
}
```

* **Resulting HTML:** `<button class="Button_button__1_a2b">Click Me</button>`
* **Best Practice:** This is a great choice for developers who like writing traditional CSS but want to avoid style conflicts between components. It is supported out-of-the-box by tools like Create React App.[^14_3][^14_2]

***

#### 2. CSS-in-JS Libraries

CSS-in-JS libraries allow you to write your styles directly within your JavaScript or TypeScript files. This co-locates your component's logic, template, and styles.

* **Analogy:** Instead of having a separate recipe book for sauces (`.css` file), you write the sauce recipe directly on the same page as the main dish recipe (`.jsx` file). This keeps everything related to one dish together.

**Popular Libraries:**


| Library | Key Idea |
| :-- | :-- |
| **styled-components** | Creates React components with styles attached, using tagged template literals to write actual CSS[^14_4][^14_5]. |
| **Emotion** | A highly performant and flexible library that offers two main approaches: a `styled` API (similar to styled-components) and a `css` prop for inline-like styling[^14_6][^14_7]. |

**`styled-components` Example:**

```jsx
import styled from 'styled-components';

// Create a <Button> component that has its own styles
const Button = styled.button`
  background: ${props => (props.$primary ? 'palevioletred' : 'white')};
  color: ${props => (props.$primary ? 'white' : 'palevioletred')};
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

// Usage
<Button>Normal</Button>
<Button $primary>Primary</Button>
```

* **React Version Note:** As of `styled-components` v5.1+, it is recommended to prefix transient props (props that are only used for styling and shouldn't be passed to the DOM) with a dollar sign (`$`), like `$primary`.[^14_4]

**Emotion (`css` prop) Example:**

```jsx
/** @jsxImportSource @emotion/react */
import { css } from '@emotion/react';

const color = 'darkturquoise';

function MyComponent() {
  return (
    <div
      css={css`
        padding: 32px;
        background-color: hotpink;
        font-size: 24px;
        border-radius: 4px;
        &:hover {
          color: ${color};
        }
      `}
    >
      Hover to change color.
    </div>
  );
}
```

* **Best Practice:** CSS-in-JS is excellent for creating highly dynamic and themeable component libraries. The ability to use JavaScript variables directly in your styles is a major advantage.[^14_8]

***

#### 3. Utility-First CSS (Tailwind CSS)

Tailwind CSS is a utility-first framework that provides a large set of pre-defined, single-purpose utility classes that you compose directly in your HTML.

* **Core Idea:** Instead of writing CSS, you apply existing classes like `flex`, `pt-4` (padding-top), and `text-center` to style your elements.[^14_9][^14_10]
* **Analogy:** Tailwind is like a set of LEGO bricks. You don't create new custom bricks for every model. Instead, you build everything by combining the standard, reusable bricks in different ways.

```jsx
// No separate CSS file is written for this component
function AlertButton() {
  return (
    <button className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
      Click Me
    </button>
  );
}
```

| Pros | Cons |
| :-- | :-- |
| **Rapid Prototyping:** Extremely fast to style components without leaving your JSX. | **"Cluttered" HTML:** The class lists can become very long and may seem unreadable at first. |
| **Consistency:** Enforces a consistent design system (spacing, colors, etc.). | **Learning Curve:** Requires learning the Tailwind class names. |
| **Performance:** Produces highly optimized, small CSS files by only including the classes you actually use. | **Less "Semantic" CSS:** You are styling behaviorally, not semantically (e.g., `text-lg` instead of `.card-title`). |

* **Best Practice:** Tailwind is a fantastic choice for projects where rapid development and a consistent design system are top priorities. It has become a dominant styling solution in the React ecosystem.[^14_11][^14_10]

***

Would you like to continue with Section 14: Accessibility (A11y)?
<span style="display:none">[^14_12][^14_13][^14_14][^14_15][^14_16][^14_17][^14_18][^14_19][^14_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^14_1]: https://www.w3schools.com/react/react_css_modules.asp

[^14_2]: https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/

[^14_3]: https://www.geeksforgeeks.org/reactjs/how-do-css-modules-help-in-styling-react-components/

[^14_4]: https://styled-components.com/docs/basics

[^14_5]: https://dev.to/elijahtrillionz/complete-guide-on-how-to-use-styled-components-in-react-360c

[^14_6]: https://emotion.sh/docs/introduction

[^14_7]: https://github.com/emotion-js/emotion

[^14_8]: https://www.tatvasoft.com/outsourcing/2025/06/emotion-reactjs.html

[^14_9]: https://www.contentful.com/blog/react-app-tailwind-css/

[^14_10]: https://tailwindcss.com/docs/installation/framework-guides

[^14_11]: https://www.yourteaminindia.com/tech-insights/guide-to-using-tailwind-css-with-react

[^14_12]: https://www.w3schools.com/react/react_css_styling.asp

[^14_13]: https://www.youtube.com/watch?v=Y1acnpuMBAw

[^14_14]: https://www.joshwcomeau.com/react/demystifying-styled-components/

[^14_15]: https://www.dhiwise.com/post/how-to-structure-and-organize-react-css-modules

[^14_16]: https://www.youtube.com/watch?v=pHi4dAXmB-4

[^14_17]: https://github.com/css-modules/css-modules

[^14_18]: https://www.reddit.com/r/reactjs/comments/1bbwts6/realworld_projects_using_css_modules/

[^14_19]: https://v3.tailwindcss.com/docs/guides/create-react-app

[^14_20]: https://www.digitalocean.com/community/tutorials/react-react-emotion


---

# yes

Of course. Let's cover Section 14.

### Accessibility (A11y)

Accessibility (often abbreviated as **a11y**) is the practice of making your web applications usable by everyone, including people with disabilities. Building accessible apps is not just a best practice; it's a crucial part of creating inclusive user experiences. React fully supports building accessible sites, primarily through standard HTML techniques.[^15_1]

***

#### 1. Semantic HTML

The foundation of an accessible website is **semantic HTML**. Using the correct HTML elements for their intended purpose gives you a huge amount of accessibility for free.[^15_1]

```
*   Use `<button>` for actions, `<a>` for navigation, `<h1>`-`<h6>` for headings, etc.
```

```
*   **Common Pitfall:** Using a `<div>` with an `onClick` handler instead of a `<button>`. A `div` is not focusable by default, doesn't have the correct ARIA role, and isn't triggered by the `Enter` or `Space` keys.
```

```
**Best Practice:** Use React Fragments (`<>...</>`) to avoid adding unnecessary `div`s that can break the semantic structure of lists (`<ul>`, `<ol>`) or tables (`<table>`).[^15_1]
```

```jsx
// Good: Preserves the <dl> structure
function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        // Fragments don't add extra nodes to the DOM
        <React.Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </React.Fragment>
      ))}
    </dl>
  );
}
```


***

#### 2. ARIA (Accessible Rich Internet Applications)

When semantic HTML isn't enough for complex, dynamic widgets, you can use ARIA attributes to add the necessary context for assistive technologies like screen readers.[^15_2][^15_3]

```
*   **Analogy:** ARIA attributes are like descriptive labels and signs in a building. While the structure (`<h1>`, `<nav>`) tells you where the rooms are, ARIA signs (`aria-label`, `role`) tell you exactly what each room is for and whether its door is open or closed.
```

* All `aria-*` attributes are fully supported in JSX and are written in **hyphen-case** (e.g., `aria-label`).[^15_1]

**Common ARIA Attributes:**


| Attribute | Purpose | Example |
| :-- | :-- | :-- |
| `role` | Defines the element's purpose (e.g., `button`, `navigation`, `dialog`)[^15_3]. | `<div role="button">...</div>` |
| `aria-label` | Provides a text label when there is no visible text[^15_4]. | `<button aria-label="Close">X</button>` |
| `aria-labelledby` | Associates an element with a text label located elsewhere on the page. | `<div role="dialog" aria-labelledby="dialogTitle">` |
| `aria-expanded` | Indicates whether a collapsible element is currently expanded or collapsed[^15_2]. | `<button aria-expanded={isOpen}>` |
| `aria-live` | Informs screen readers about dynamic content changes (e.g., live chat, error messages)[^15_4]. | `<div aria-live="polite">New message received</div>` |

* **Common Pitfall:** Using ARIA to replicate semantics that already exist. The first rule of ARIA is: if a native HTML element has the behavior and semantics you need, use it instead.

***

#### 3. Keyboard Navigation and Focus Management

All interactive functionality must be accessible using only a keyboard.[^15_5][^15_1]

* **Focus Order:** Ensure the tab order is logical and intuitive. It should follow the visual flow of the page.
* **Visible Focus Indicator:** Never remove the focus outline (`outline: 0`) without providing a clear, high-contrast alternative. Users need to see where they are on the page.[^15_1]

**Programmatic Focus Management**

For dynamic UIs, you must manage focus yourself to prevent it from being lost. Use `useRef` to set focus imperatively.[^15_5]

* **Use Case:** When a modal opens, focus should move to the first interactive element inside it. When it closes, focus should return to the element that opened it.

```jsx
function Modal({ onClose }) {
  const closeButtonRef = useRef(null);

  useEffect(() => {
    // Focus the close button when the modal mounts
    closeButtonRef.current?.focus();
  }, []);
  
  return (
    <div>
      {/* ... modal content ... */}
      <button ref={closeButtonRef} onClick={onClose}>Close</button>
    </div>
  );
}
```


***

#### 4. Screen Readers

Screen readers are software that reads the content of a screen aloud, used primarily by people with visual impairments.[^15_6][^15_7]

* **Image `alt` Text:** Always provide descriptive `alt` text for images. If an image is purely decorative, use an empty `alt=""` so screen readers will ignore it.[^15_4]
* **Accessible Forms:** Use the `<label>` element and associate it with its input using the `htmlFor` attribute in JSX. This ensures screen readers announce the label when the user focuses on the input.[^15_1]

```jsx
<label htmlFor="name-input">Name:</label>
<input id="name-input" type="text" />
```


***

#### Best Practices \& Tools

* **Testing is Non-Negotiable:** The most important check is to unplug your mouse and try to use your entire application with just the keyboard.[^15_1]
* **Use Screen Readers:** Test your application with real screen readers like **NVDA** (Windows, free), **JAWS** (Windows, paid), and **VoiceOver** (macOS/iOS, built-in).[^15_2]
* **Automated Tools:**
    * **`eslint-plugin-jsx-a11y`**: Provides real-time feedback on accessibility issues directly in your editor. It's included in Create React App by default.[^15_1]
    * **Browser Extensions:** Tools like **axe DevTools** and **Lighthouse** can audit your pages and catch common accessibility violations.

***

Would you like to continue with Section 15: Internationalization (i18n)?
<span style="display:none">[^15_10][^15_11][^15_12][^15_13][^15_14][^15_15][^15_16][^15_17][^15_18][^15_19][^15_20][^15_8][^15_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^15_1]: https://legacy.reactjs.org/docs/accessibility.html

[^15_2]: https://www.uxpin.com/studio/blog/how-react-components-enhance-screen-reader-accessibility/

[^15_3]: https://www.geeksforgeeks.org/reactjs/aria-attributes-in-react-accessibility/

[^15_4]: https://dev.to/rowsanali/accessibility-in-react-applications-best-practices-and-tools-3ck4

[^15_5]: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Frameworks_libraries/React_accessibility

[^15_6]: https://www.geeksforgeeks.org/reactjs/react-mui-screen-readers/

[^15_7]: https://www.w3schools.com/accessibility/accessibility_screen_readers.php

[^15_8]: https://www.geeksforgeeks.org/reactjs/accessibility-in-reactjs/

[^15_9]: https://www.tiny.cloud/blog/react-accessibility/

[^15_10]: https://www.telerik.com/kendo-react-ui/components/common/navigation

[^15_11]: https://www.angularminds.com/blog/web-accessibility-in-reactjs

[^15_12]: https://whereisthemouse.com/create-a-list-component-with-keyboard-navigation-in-react

[^15_13]: https://www.reddit.com/r/react/comments/1din1wj/how_to_implement_screen_reader_functionality_in/

[^15_14]: https://www.reddit.com/r/reactjs/comments/1hxcd2h/accessibility_essentials_every_react_developer/

[^15_15]: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles

[^15_16]: https://www.freecodecamp.org/news/designing-keyboard-accessibility-for-complex-react-experiences/

[^15_17]: https://mui.com/system/screen-readers/

[^15_18]: https://reactnative.dev/docs/accessibility

[^15_19]: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Guides/Techniques

[^15_20]: https://www.ag-grid.com/react-data-grid/keyboard-navigation/


---

# yes

Of course. Here is the revision guide for Section 15.

### Internationalization (i18n)

Internationalization (i18n) is the process of designing an application so that it can be adapted to various languages and regions without engineering changes. Localization (l10n) is the process of adapting it for a *specific* region. In React, this is typically handled by dedicated libraries that manage translations, formatting, and locale switching.[^16_1]

#### Core Concepts

* **Translation Keys:** Instead of hardcoding text, you use a unique key (e.g., `"header.title"`). The library then looks up the correct translation for that key based on the current language.
* **Locale Files:** Translations are stored in files, usually JSON, one for each language (e.g., `en.json`, `es.json`).[^16_2]
* **Provider:** A top-level component (e.g., `<IntlProvider>`) wraps your app, providing the i18n context (current locale, translation messages) to all child components.[^16_2]
* **ICU Message Syntax:** A standardized format used by libraries like `react-intl` for handling complex translations, including variables, plurals, and genders.[^16_3][^16_1]

***

#### Popular i18n Libraries

| Feature | `react-intl` (Part of FormatJS) | `react-i18next` |
| :-- | :-- | :-- |
| **Philosophy** | A collection of React components and an API focused on the powerful **ICU message format**[^16_4][^16_3]. | A complete framework built on top of the highly versatile **`i18next` core**, which is framework-agnostic[^16_5][^16_6]. |
| **Primary Usage** | Component-based (`<FormattedMessage>`) and hook-based (`useIntl()`)[^16_4]. | Hook-based (`useTranslation()` hook and `t()` function), with a `<Trans>` component for complex cases involving JSX[^16_5]. |
| **Ecosystem** | Part of the broader **FormatJS** suite, which provides polyfills for standard `Intl` APIs[^16_7]. | Benefits from the large `i18next` ecosystem, including plugins for language detection and backends for loading translations[^16_5]. |
| **Learning Curve** | Generally straightforward, especially if you focus on the component API[^16_8]. | Slightly more configuration upfront but very powerful and flexible[^16_9]. |


***

#### `react-intl` Example

1. **Setup:** Wrap your app in `IntlProvider` and provide the `locale` and `messages`.
```jsx
// App.js
import { IntlProvider } from 'react-intl';
import messages_en from './locales/en.json';
import messages_fr from './locales/fr.json';

const messages = {
  en: messages_en,
  fr: messages_fr,
};

function App() {
  const [locale, setLocale] = useState('en');

  return (
    <IntlProvider locale={locale} messages={messages[locale]}>
      {/* ... rest of your app ... */}
    </IntlProvider>
  );
}
```

2. **Usage:** Use the `<FormattedMessage>` component.
```jsx
import { FormattedMessage } from 'react-intl';

const Greeting = () => (
  <h1>
    <FormattedMessage
      id="app.greeting"
      defaultMessage="Hello, World!" // Fallback text
    />
  </h1>
);
```


***

#### `react-i18next` Example

1. **Setup:** Create a configuration file.
```javascript
// i18n.js
import i18n from 'i18next';
import { initReactI18next } from 'react-i18next';
import en from './locales/en.json';
import fr from './locales/fr.json';

i18n.use(initReactI18next).init({
  resources: {
    en: { translation: en },
    fr: { translation: fr },
  },
  lng: 'en', // Default language
  fallbackLng: 'en',
  interpolation: { escapeValue: false },
});

export default i18n;
```

2. **Usage:** Use the `useTranslation` hook.
```jsx
import { useTranslation } from 'react-i18next';

function Greeting() {
  const { t, i18n } = useTranslation();

  const changeLanguage = (lng) => {
    i18n.changeLanguage(lng);
  };

  return <h1>{t('app.greeting')}</h1>;
}
```


***

#### Formatting (Dates, Numbers, and Plurals)

A crucial part of i18n is correctly formatting data based on locale.


| Formatting | `react-intl` | `react-i18next` |
| :-- | :-- | :-- |
| **Numbers** | Uses components like `<FormattedNumber value={1000} />`[^16_10]. | Uses built-in formatting with the `Intl` API: `t('key', { val: 1000, format: 'number' })`[^16_11]. |
| **Dates** | Uses `<FormattedDate value={new Date()} />` or `<FormattedRelativeTime />`[^16_3]. | Similar to numbers, uses the `Intl.DateTimeFormat` API: `t('key', { date: new Date(), format: 'date' })`[^16_11]. |
| **Plurals** | Uses ICU message syntax directly in the translation string: `'You have {count, plural, one {# message} other {# messages}}'`[^16_3]. | Uses special keys in the JSON file (`key_one`, `key_other`) and a `count` option: `t('key', { count: 1 })`[^16_12]. |

#### Best Practices \& Pitfalls

* **Best Practice:** Always provide a `defaultMessage` (in `react-intl`) or a `fallbackLng` (in `i18next`) to handle missing translations gracefully.
* **Best Practice:** For large applications, use a translation management system (TMS) to manage translation files. `i18next` heavily promotes **Locize** for this.[^16_5]
* **Common Pitfall:** Concatenating strings and variables (e.g., `t('You have') + count + t('messages')`). This breaks grammar in many languages. Always use the library's built-in interpolation and pluralization features.
* **Common Pitfall:** Forgetting to account for Right-to-Left (RTL) languages like Arabic or Hebrew, which requires CSS changes (e.g., `flex-direction: row-reverse`).

***

Would you like to continue with Section 16: Testing?
<span style="display:none">[^16_13][^16_14][^16_15][^16_16][^16_17][^16_18][^16_19][^16_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^16_1]: https://www.angularminds.com/blog/introduction-to-internationalization-in-react-apps

[^16_2]: https://www.telerik.com/blogs/internationalization-react-intl

[^16_3]: https://github.com/ericf/react-intl

[^16_4]: https://formatjs.github.io/docs/react-intl/

[^16_5]: https://react.i18next.com

[^16_6]: https://github.com/i18next/react-i18next

[^16_7]: https://github.com/formatjs/formatjs

[^16_8]: https://localizely.com/blog/react-intl-tutorial/

[^16_9]: https://phrase.com/blog/posts/localizing-react-apps-with-i18next/

[^16_10]: https://phrase.com/blog/posts/react-i18n-format-js/

[^16_11]: https://www.i18next.com/translation-function/formatting

[^16_12]: https://lokalise.com/blog/how-to-internationalize-react-application-using-i18next/

[^16_13]: https://blog.logrocket.com/react-intl-internationalize-your-react-apps/

[^16_14]: https://lokalise.com/blog/react-i18n-intl/

[^16_15]: https://buttercms.com/blog/react-intl-an-api-and-component-analysis/

[^16_16]: https://www.creolestudios.com/react-i18next-simplifying-internationalization-in-react/

[^16_17]: https://testing-library.com/docs/example-react-intl/

[^16_18]: https://www.youtube.com/watch?v=U4_P_l3L_EA

[^16_19]: https://ej2.syncfusion.com/react/documentation/common/globalization/internationalization

[^16_20]: https://storybook.js.org/recipes/react-i18next


---

# yes

Of course. Let's proceed with Section 16.

### Testing

Testing in React ensures your application is reliable, maintainable, and bug-free. The modern testing philosophy focuses on simulating user behavior rather than testing internal implementation details.

#### The Testing Philosophy: React Testing Library (RTL)

The guiding principle of React Testing Library is simple:

> "The more your tests resemble the way your software is used, the more confidence they can give you."[^17_1]

This means your tests should interact with your components from a user's perspective.

* **Do:** Find elements by their text content, label, or accessibility role (e.g., "button").
* **Don't:** Rely on implementation details like CSS class names, component state, or prop values.


#### The Testing Stack

A standard React testing environment typically includes:

* **Jest:** A test runner that provides the testing framework, assertion functions (`expect`), and powerful mocking capabilities.[^17_2][^17_3]
* **React Testing Library (RTL):** A library for rendering components and interacting with them in a way that mimics user actions.[^17_4]
* **`@testing-library/jest-dom`:** An extension that adds convenient, DOM-specific matchers to Jest, such as `toBeInTheDocument()` and `toBeVisible()`.[^17_3]
* **`@testing-library/user-event`:** A companion library for simulating more realistic user interactions like typing and hovering.


#### Unit \& Integration Testing with Jest and RTL

This is the most common form of testing for React components, focusing on individual pieces (unit) or small groups of components working together (integration).

**Example: Testing a simple Counter**

```jsx
// Counter.js
import React, { useState } from 'react';

export function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

// Counter.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import { Counter } from './Counter';

describe('Counter component', () => {
  test('renders with an initial count of 0', () => {
    render(<Counter />);
    // Find elements by what the user sees
    expect(screen.getByText('Count: 0')).toBeInTheDocument();
  });

  test('increments the count when the button is clicked', () => {
    render(<Counter />);
    const button = screen.getByRole('button', { name: /increment/i });
    
    // Simulate a user click
    fireEvent.click(button);
    
    // Assert that the UI updated correctly
    expect(screen.getByText('Count: 1')).toBeInTheDocument();
  });
});
```

* **Best Practice:** Prioritize queries that are accessible to users, such as `getByRole`, `getByLabelText`, or `getByText`. Avoid `getByTestId` unless no other selector is practical.[^17_4]


#### Mocking APIs

Tests need to be fast and deterministic, so they should not make actual network requests. Jest provides built-in functions to mock API calls.[^17_5]

```jsx
// Mocking the global fetch function
global.fetch = jest.fn(() =>
  Promise.resolve({
    json: () => Promise.resolve({ name: 'John Doe' }),
  })
);

test('displays the user name after data is fetched', async () => {
  render(<UserProfile />);
  
  // Use `findBy` queries for elements that appear asynchronously
  const userNameElement = await screen.findByText('John Doe');
  expect(userNameElement).toBeInTheDocument();
  
  // Verify that the mocked fetch was called
  expect(global.fetch).toHaveBeenCalledTimes(1);
});
```

* **`getBy*`**: Throws an error if the element is not found. Use it for elements you expect to be present.
* **`queryBy*`**: Returns `null` if the element is not found. Use it to assert that an element is *not* on the screen.
* **`findBy*`**: Returns a promise that resolves when the element appears. Use it for asynchronous UI updates.


#### End-to-End (E2E) Testing with Cypress

E2E tests automate a real browser to simulate a complete user journey through your application. **Cypress** is a popular, developer-friendly tool for this.[^17_6]

* **Analogy:** While unit tests check if a single car engine part works, an E2E test puts a person in the driver's seat and has them drive the car from home to work, ensuring the entire system functions correctly.

**Example Cypress Test:**

```javascript
// cypress/e2e/login.cy.js
describe('Login Flow', () => {
  it('allows a user to log in and redirects them to the dashboard', () => {
    // 1. Visit the login page
    cy.visit('/login');

    // 2. Find form elements and interact with them
    cy.get('input[name="email"]').type('test@example.com');
    cy.get('input[name="password"]').type('password123');
    cy.get('button[type="submit"]').click();

    // 3. Assert the outcome
    cy.url().should('include', '/dashboard');
    cy.contains('h1', 'Welcome to your Dashboard').should('be.visible');
  });
});
```

* **Best Practice:** Reserve E2E tests for the most critical user paths, such as authentication or checkout flows. They are more powerful but also slower and more expensive to maintain than unit or integration tests.[^17_7]

***

Would you like to continue with Section 17: Server-Side Rendering \& Streaming?
<span style="display:none">[^17_10][^17_11][^17_12][^17_13][^17_14][^17_15][^17_16][^17_17][^17_18][^17_19][^17_20][^17_8][^17_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^17_1]: https://testing-library.com/docs/guiding-principles/

[^17_2]: https://daily.dev/blog/react-js-jest-beginners-guide

[^17_3]: https://www.browserstack.com/guide/react-app-testing-with-jest

[^17_4]: https://daily.dev/blog/react-functional-testing-best-practices

[^17_5]: https://www.linkedin.com/pulse/mocking-api-calls-react-tests-jest-dhanesh-mane-qqb5f

[^17_6]: https://bugfender.com/blog/how-to-perform-an-end-to-end-test-of-a-react-app-using-cypress/

[^17_7]: https://www.freecodecamp.org/news/cypress-for-end-to-end-testing-react-apps/

[^17_8]: https://jestjs.io/docs/tutorial-react

[^17_9]: https://www.youtube.com/watch?v=JBSUgDxICg8

[^17_10]: https://create-react-app.dev/docs/running-tests/

[^17_11]: https://keploy.io/blog/community/a-guide-to-testing-react-components-with-jest-and-react-testing-library

[^17_12]: https://kentcdodds.com/blog/common-mistakes-with-react-testing-library

[^17_13]: https://docs.cypress.io/app/end-to-end-testing/writing-your-first-end-to-end-test

[^17_14]: https://refine.dev/blog/mocking-api-calls-in-react/

[^17_15]: https://testing-library.com/docs/react-testing-library/intro

[^17_16]: https://www.browserstack.com/guide/mock-api-setup-react

[^17_17]: https://jestjs.io

[^17_18]: https://testing-library.com/docs/queries/about/

[^17_19]: https://dev.to/clickpesa/react-write-end-to-end-test-using-cypress-3450

[^17_20]: https://stackoverflow.com/questions/55657971/how-to-mock-api-calls-made-within-a-react-component-being-tested-with-jest


---

# yes

Of course. Let's delve into Section 17.

### Server-Side Rendering \& Streaming

This section covers how React applications can be rendered on the server to improve performance and SEO, focusing on modern techniques introduced in React 18 and popularized by frameworks like Next.js.[^18_1]

#### What is Server-Side Rendering (SSR)?

SSR is the process of rendering your React components into HTML on the **server** for each request. The fully-formed HTML page is then sent to the browser, so the user sees content immediately, even before any JavaScript has downloaded or executed.[^18_2][^18_1]

**SSR vs. Client-Side Rendering (CSR):**

```
*   **CSR (the default for Create React App):** The server sends a minimal HTML file with a `<div id="root"></div>` and a large JavaScript bundle. The browser downloads the JS, and then React builds the entire UI on the client.
```

* **SSR:** The server sends a complete HTML page. The browser displays it instantly, then downloads the JS in the background to make the page interactive.[^18_3]

**Why use SSR?**

* **Faster Perceived Performance:** Users see meaningful content much faster, improving the "First Contentful Paint" (FCP) metric.
* **Better SEO:** Search engine crawlers can easily index the fully-rendered HTML content, which can be difficult with client-rendered apps.[^18_4]

***

#### Hydration: Making the HTML Interactive

The HTML sent from the server is just a static snapshot. It's not interactive. **Hydration** is the client-side process where React "attaches" event handlers and initializes state for the server-rendered HTML, turning it into a fully functional React application.[^18_5][^18_6][^18_7]

* **Analogy:** SSR sends you a beautiful, fully-assembled model car (the HTML). Hydration is the process of adding the engine, battery, and remote control receiver (the JavaScript logic and event handlers) so you can actually drive it.
* **React 18 API:** In React 18, you use `hydrateRoot` instead of the old `ReactDOM.hydrate`.[^18_8][^18_9]

```jsx
// client-entry.js
import { hydrateRoot } from 'react-dom/client';
import App from './App';

hydrateRoot(document.getElementById('root'), <App />);
```

* **Common Pitfall:** A **hydration mismatch** occurs if the component output on the client's initial render is different from the server-rendered HTML (e.g., due to using `window.innerWidth` or rendering a `new Date()`). This can cause bugs and performance issues. React expects the server and client HTML to match perfectly.[^18_6]

***

#### Next.js: The Production Framework for SSR

**Next.js** is a React framework that makes implementing SSR straightforward.

* **Pages Router:** In the older `pages` directory, you export an `async` function called `getServerSideProps` from a page. Next.js will run this function on the server for every request, passing the fetched data as props to your page component.[^18_10][^18_4]
* **App Router:** In the newer `app` directory, all components are **Server Components** by default, which means they are automatically server-rendered. This simplifies the mental model significantly.[^18_11]

***

### React 18 Streaming SSR

A limitation of traditional SSR is that you can't send any HTML until the entire page is ready on the server. If one data fetch is slow, it blocks the whole page.

**Streaming SSR**, introduced in React 18, solves this. It allows the server to send the HTML in chunks as they become ready.[^18_11][^18_8]

* **How it works:** You wrap slow parts of your UI in a `<Suspense>` boundary. React will send the HTML for the fast parts immediately, along with a placeholder (your `fallback` UI) for the slow part. Once the data for the slow part is ready on the server, React sends the HTML for that component in the same stream, along with a tiny script to "pop" it into place.
* **React 18 API:** `renderToPipeableStream` (for Node.js environments) and `renderToReadableStream` (for edge runtimes) are the new APIs that enable streaming.[^18_12][^18_13]

**Streaming in Next.js:**
The Next.js App Router has streaming built-in. By using `loading.js` files or `<Suspense>` boundaries, you can easily create streaming UIs where parts of the page load progressively without blocking the rest of the content.[^18_14][^18_11]

**Benefits of Streaming:**

* **Faster Time to First Byte (TTFB):** The browser starts receiving HTML almost instantly.
* **Improved User Experience:** The user sees the main layout and content quickly and can interact with it while slower, non-essential parts of the page are still loading.

***

Would you like to continue with Section 18: React 18+ and 19 Features?
<span style="display:none">[^18_15][^18_16][^18_17][^18_18][^18_19][^18_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^18_1]: https://www.reddit.com/r/nextjs/comments/1esoz63/whats_the_motivation_behind_serverside_rendering/

[^18_2]: https://nextjs.org/docs/pages/building-your-application/rendering/server-side-rendering

[^18_3]: https://www.geeksforgeeks.org/nextjs/what-is-ssr-in-nextjs/

[^18_4]: https://www.freecodecamp.org/news/server-side-rendering-in-next-js-for-improved-seo/

[^18_5]: https://www.greatfrontend.com/questions/quiz/explain-what-react-hydration-is

[^18_6]: https://react.dev/reference/react-dom/client/hydrateRoot

[^18_7]: https://www.gatsbyjs.com/docs/conceptual/react-hydration/

[^18_8]: https://react.dev/blog/2022/03/29/react-v18

[^18_9]: https://dev.to/jitendrachoudhary/what-is-react-hydration-2bc3

[^18_10]: https://www.turing.com/kb/nextjs-server-side-rendering

[^18_11]: https://blog.appsignal.com/2023/12/13/server-side-rendering-with-nextjs-react-and-typescript.html

[^18_12]: https://github.com/styled-components/styled-components/issues/3658

[^18_13]: https://react.dev/reference/react-dom/server/renderToPipeableStream

[^18_14]: https://nextjs.org/docs/14/app/building-your-application/rendering/server-components

[^18_15]: https://nextjs.org/docs/app/getting-started/server-and-client-components

[^18_16]: https://blog.logrocket.com/streaming-ssr-with-react-18/

[^18_17]: https://www.youtube.com/watch?v=R8ZwbehCGP0

[^18_18]: https://react.dev/reference/react-dom/hydrate

[^18_19]: https://github.com/reactwg/react-18/discussions/37

[^18_20]: https://www.reddit.com/r/reactjs/comments/18fky3q/what_is_hydration_in_react/


---

# yes

Of course. Here is the revision guide for Section 18.

### React 18+ and 19 Features

React 18 laid the groundwork for a new era of user experience with concurrent features, while React 19 builds on this foundation with powerful new hooks and the stabilization of Server Components.

***

### Key Features from React 18

#### 1. Concurrent Rendering

This is the foundational, "behind-the-scenes" change in React 18. Concurrency allows React to prepare multiple versions of the UI at the same time. It can pause, resume, or abandon a render, which makes React apps feel much more responsive.[^19_1][^19_2][^19_3]

* **Analogy:** Before concurrency, rendering was like a single-track phone call; you couldn't do anything else until the call was finished. Concurrent rendering is like having call waiting; React can "pause" a long, low-priority render to handle an urgent incoming one (like user input) and then resume the first one later.[^19_3]
* **Activation:** Concurrency is enabled automatically when you use a feature that needs it, like `useTransition` or streaming SSR.[^19_2]


#### 2. `useTransition`

This hook lets you mark certain state updates as non-urgent "transitions." React will keep the UI interactive while the transition is rendering in the background.[^19_4]

* **Syntax:** `const [isPending, startTransition] = useTransition();`
    * `isPending`: A boolean that tells you if the transition is currently happening (useful for showing loading spinners).
    * `startTransition`: A function you wrap around a state update to mark it as a transition.[^19_5]

**Example: Filtering a large list without blocking input**

```jsx
const [inputValue, setInputValue] = useState('');
const [searchQuery, setSearchQuery] = useState('');
const [isPending, startTransition] = useTransition();

const handleChange = (e) => {
  // Urgent: Update the input field immediately
  setInputValue(e.target.value);
  
  // Non-urgent: Start a transition to update the search results.
  // This can be interrupted if the user keeps typing.
  startTransition(() => {
    setSearchQuery(e.target.value);
  });
};

return (
  <div>
    <input value={inputValue} onChange={handleChange} />
    {isPending && <p>Loading...</p>}
    <MySlowList query={searchQuery} />
  </div>
);
```


#### 3. Automatic Batching

In React 18, all state updates are automatically batched, no matter where they originate (e.g., inside promises, `setTimeout`, or native event handlers). This means multiple state updates will trigger only a single re-render, improving performance out-of-the-box.[^19_6]

#### 4. `useId`

A hook for generating unique, stable IDs that are consistent on both the server and the client. This is crucial for accessibility and avoiding hydration mismatches.[^19_7][^19_8]

```
*   **Use Case:** Linking a `<label>` to an `<input>` with `htmlFor` and `id`.[^19_9]
```

```jsx
import { useId } from 'react';

function FormField() {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>Your Name</label>
      <input id={id} type="text" />
    </>
  );
}
```


***

### New Features in React 19

React 19, currently in canary, builds on these ideas and introduces powerful new capabilities.

#### 1. Server Components \& Actions

* **Server Components:** These are a new type of component that runs exclusively on the server, either at build time or per request. They can access server-side resources directly (like databases or file systems) and they send **zero JavaScript** to the client, reducing bundle sizes and improving load times.[^19_10][^19_11]
* **`"use client"` directive:** You use this directive at the top of a file to mark components that need to be interactive and run on the client (e.g., components with `useState` or `useEffect`).
* **Server Actions:** These are functions that run on the server but can be called from client components. They are defined with the `"use server"` directive and simplify data mutations (e.g., form submissions) by allowing you to write server-side logic that feels like a local function call.


#### 2. New `use` Hook Family

React 19 introduces several new hooks for simplifying common patterns.[^19_12]

* **`use` Hook:** A versatile hook that can read the value of a promise (integrating with `<Suspense>`) or a context. This allows for cleaner data fetching in Server Components and conditional context consumption.[^19_12]
* **`useFormStatus` Hook:** Allows a component to access status information about the parent `<form>` it's inside, such as whether the form is currently submitting (`pending`). This is great for disabling buttons or showing loading states without prop drilling.[^19_13]
* **`useOptimistic` Hook:** Simplifies optimistic UI updates. You can immediately show a "successful" state to the user while the actual async operation (like a form submission) is still in flight. React will automatically revert to the real state if the operation fails.[^19_13]

***

Would you like to continue with Section 19: React + Web Workers?
<span style="display:none">[^19_14][^19_15][^19_16][^19_17][^19_18][^19_19][^19_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^19_1]: https://legacy.reactjs.org/blog/2022/03/29/react-v18.html

[^19_2]: https://www.freecodecamp.org/news/react-18-new-features/

[^19_3]: https://www.telerik.com/blogs/concurrent-rendering-react-18

[^19_4]: https://inside.caratlane.com/exploring-the-power-of-usetransition-in-react-18-824496396586

[^19_5]: https://react.dev/reference/react/useTransition

[^19_6]: https://www.dhiwise.com/post/deep-dive-into-react-concurrent-mode-exploring-key-features-and-use-cases

[^19_7]: https://www.greatfrontend.com/questions/quiz/what-is-the-useid-hook-in-react-and-when-should-it-be-used

[^19_8]: https://www.telerik.com/blogs/react-useid-hook

[^19_9]: https://refine.dev/blog/react-useid/

[^19_10]: https://metadesignsolutions.com/server-components-in-react-19-are-they-full-stack-game-changers/

[^19_11]: https://react.dev/reference/rsc/server-components

[^19_12]: https://blog.saeloun.com/2024/06/05/new-hooks-in-react-19/

[^19_13]: https://www.geeksforgeeks.org/reactjs/react-19-new-features-and-updates/

[^19_14]: https://www.curiosum.com/blog/performance-optimization-with-react-18-concurrent-rendering

[^19_15]: https://vercel.com/blog/how-react-18-improves-application-performance

[^19_16]: https://react.dev/blog/2024/12/05/react-19

[^19_17]: https://www.youtube.com/watch?v=edN42P_vfCI

[^19_18]: https://dev.to/ahmed_aarafa/your-guide-to-use-react-18-hooks-usetransition-and-usedeferredvalue-52d1

[^19_19]: https://www.reddit.com/r/reactjs/comments/1gwszdu/how_does_react_19_execute_server_components_and/

[^19_20]: https://buttercms.com/blog/react-concurrent-mode-the-future-of-web-apps/


---

# yes

Of course. Here is the revision guide for Section 19.

### React + Web Workers

Web Workers are a browser feature that allows you to run JavaScript scripts in a background thread, separate from the main thread that handles the UI. This is crucial for preventing the UI from freezing during long-running, CPU-intensive tasks.[^20_1][^20_2]

**Analogy:** The main UI thread is a busy chef in a kitchen. If they have to spend 10 minutes grinding spices by hand (a heavy computation), they can't do anything else, and customer orders pile up (the UI becomes unresponsive). A Web Worker is like hiring a kitchen assistant. The chef can hand off the spice-grinding task to the assistant (the worker thread), and continue taking orders and cooking (keeping the UI interactive). Once the assistant is done, they hand the spices back to the chef.

***

#### Why Use Web Workers in React?

The primary goal is to maintain a smooth user experience by offloading heavy tasks from the main thread.[^20_3]

**Ideal Use Cases:**

* **Complex Calculations:** Processing large datasets, performing complex mathematical or financial calculations.
* **Data Processing:** Parsing large JSON files, processing images or videos on the client-side.
* **Background Tasks:** Data synchronization, text analysis, or any computation that takes more than a few milliseconds.

***

#### Basic Implementation

The native Web Worker API relies on a message-passing system.

1. **Create the Worker File:** This is a separate JavaScript file that contains the heavy logic.
```javascript
// heavy-calculation.worker.js
self.onmessage = function (event) {
  console.log('Worker: Message received from main script');
  const number = event.data;
  const result = number * 2; // Simulate a heavy task
  
  console.log('Worker: Posting message back to main script');
  self.postMessage(result);
};
```

2. **Use the Worker in a React Component:**
```jsx
import React, { useState, useEffect, useRef } from 'react';

function WorkerComponent() {
  const [result, setResult] = useState(null);
  const workerRef = useRef(null);

  useEffect(() => {
    // Initialize the worker
    workerRef.current = new Worker(new URL('./heavy-calculation.worker.js', import.meta.url));

    // Listen for messages from the worker
    workerRef.current.onmessage = (event) => {
      setResult(event.data);
    };

    // Cleanup: Terminate the worker when the component unmounts
    return () => {
      workerRef.current.terminate();
    };
  }, []);

  const runCalculation = () => {
    // Send a message to the worker to start the task
    workerRef.current.postMessage(10);
  };

  return (
    <div>
      <button onClick={runCalculation}>Run Heavy Calculation</button>
      {result && <p>Result from worker: {result}</p>}
    </div>
  );
}
```

* **Common Pitfall:** Forgetting to terminate the worker on component unmount (`worker.terminate()`). This can lead to memory leaks as the worker thread continues to run in the background.[^20_1]

***

#### Simplifying Workers with Libraries

The raw `postMessage` API can be cumbersome. Libraries exist to make worker communication feel more natural.


| Library | Key Idea |
| :-- | :-- |
| **Comlink** | A library by Google that makes Web Workers easier to use by abstracting away the `postMessage` details. It lets you call functions on your worker as if they were local `async` functions[^20_4]. |
| **`workerize-loader`** | A webpack loader that lets you `import` a module and automatically runs it in a worker, exposing its exported functions[^20_5]. |
| **`use-worker`** | A React hook that simplifies the process of running computations in a worker, providing status updates (e.g., `IDLE`, `RUNNING`, `SUCCESS`)[^20_6]. |

**Comlink Example:**

Comlink makes your worker code feel like a remote procedure call (RPC).

```javascript
// my-worker.js
import { expose } from 'comlink';

const calculator = {
  add(a, b) {
    return a + b;
  }
};

expose(calculator);
```

```jsx
// MyComponent.jsx
import { wrap } from 'comlink';
import { useEffect, useState } from 'react';

const worker = new Worker(new URL('./my-worker.js', import.meta.url));
const workerApi = wrap(worker);

function MyComponent() {
  const [total, setTotal] = useState(0);

  useEffect(() => {
    async function calculate() {
      // Call the worker function like a normal async function!
      const result = await workerApi.add(5, 10);
      setTotal(result);
    }
    calculate();
  }, []);
  
  return <p>Total: {total}</p>;
}
```


***

#### Best Practices \& Pitfalls

* **Best Practice:** Encapsulate worker logic within a custom hook (e.g., `useHeavyCalculation`) to make it reusable and keep your components clean.[^20_7]
* **Common Pitfall:** Trying to access the `window` or `document` objects inside a worker. Web Workers run in a separate global scope and do not have access to the DOM.[^20_2]
* **Best Practice:** Use a library like **Comlink** for any non-trivial worker implementation. The improved developer experience and reduced boilerplate are well worth it.[^20_8]
* **Don't Overuse:** Workers add complexity. Only use them for tasks that genuinely block the main thread. For I/O-bound tasks like fetching data, standard `async/await` is usually sufficient.

***

Would you like to continue with Section 20: Error \& Performance Diagnostics?
<span style="display:none">[^20_10][^20_11][^20_12][^20_13][^20_14][^20_15][^20_16][^20_17][^20_18][^20_19][^20_20][^20_9]</span>

```
<div style="text-align: center">⁂</div>
```

[^20_1]: https://dev.to/sumankalia/web-workers-in-reactjs-4bc7

[^20_2]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers

[^20_3]: https://www.dhiwise.com/post/power-of-web-workers-in-react-for-improved-user-experience

[^20_4]: https://blog.logrocket.com/integrating-web-workers-in-a-react-app-with-comlink/

[^20_5]: https://www.jbs.dev/resources/resource-center/blog/simple-pattern-adding-web-worker-react/

[^20_6]: https://github.com/alewin/useWorker

[^20_7]: https://www.youtube.com/watch?v=yPAp1h0vk-s

[^20_8]: https://johnnyreilly.com/web-workers-comlink-vite-tanstack-query

[^20_9]: https://blog.logrocket.com/web-workers-react-typescript/

[^20_10]: https://github.com/pocesar/react-use-comlink

[^20_11]: https://dev.to/hamzakhan/how-to-use-web-workers-for-optimized-react-apps-27l3

[^20_12]: https://dev.to/gkampitakis/react-web-workers-to-the-rescue-2cmd

[^20_13]: https://www.npmjs.com/package/@shopify/react-web-worker

[^20_14]: https://github.com/gpolyn/react-and-workerize-loader

[^20_15]: https://stackoverflow.com/questions/69715751/using-google-comlink-for-web-workers-with-react-typescript-results-in-dom-except

[^20_16]: https://github.com/developit/workerize-loader/issues/5

[^20_17]: https://surma.dev/things/react-redux-comlink/

[^20_18]: https://stackoverflow.com/questions/61815764/workerize-loader-failed-to-work-after-compiling-react-typescript

[^20_19]: http://josephbeuysmum.co.uk/using-the-comlink-library-to-add-a-web-worker-in-react/

[^20_20]: https://www.gatsbyjs.com/plugins/gatsby-plugin-workerize-loader/


---

# yes

Of course. Here is the revision guide for Section 20.

### Error \& Performance Diagnostics

Effective diagnostics are crucial for building and maintaining robust, high-performance React applications. This involves using the right tools to identify performance bottlenecks, debug component behavior, and track errors in production.[^21_1]

***

### 1. React DevTools

This is an essential browser extension (for Chrome, Firefox, and Edge) that provides deep insight into your React component tree.[^21_2][^21_3]

**Key Features:**

* **Components Tab:**
    * **Inspect Component Tree:** View the hierarchy of your components, just like the DOM tree.[^21_3]
    * **View \& Edit State/Props:** Select a component to see its current props, state, and hooks. You can even edit these values in real-time to test different scenarios.[^21_1]
    * **Highlight Updates:** A killer feature for performance tuning. Enable "Highlight updates when components render" in the settings to see a visual flash on components as they re-render. This makes it easy to spot unnecessary renders.[^21_4]
* **Profiler Tab:**
    * **Record Performance:** The Profiler lets you record interactions with your app and then analyze the rendering performance.
    * **Flame \& Ranked Charts:** It provides visualizations (flamegraphs) that show which components took the longest to render and why a component re-rendered (e.g., props changed, state changed).[^21_3]
    * **Identify Bottlenecks:** This is the primary tool for answering the question, "Why is my app slow?".[^21_1]

**Best Practice:** Make the React DevTools your first stop for any debugging or performance investigation. Understanding why and when your components render is the most important skill for optimization.[^21_5]

***

### 2. The `<Profiler>` API

While the DevTools Profiler is interactive, the `<Profiler>` component API allows you to collect performance measurements programmatically. This can be useful for logging performance data over time.[^21_6][^21_7]

* **How it works:** You wrap a part of your component tree with `<Profiler>` and provide an `onRender` callback. React will call this function with detailed timing information every time the wrapped tree "commits" an update.[^21_8]

```jsx
import React, { Profiler } from 'react';

function onRenderCallback(
  id, // the "id" prop of the Profiler tree that has just committed
  phase, // "mount" (if the tree just mounted) or "update" (if it re-rendered)
  actualDuration, // time spent rendering the committed update
  // ... other metrics
) {
  // Log performance data to an analytics service
  console.log({ id, phase, actualDuration });
}

function App() {
  return (
    <Profiler id="MyComponent" onRender={onRenderCallback}>
      <MyComponent />
    </Profiler>
  );
}
```

* **Common Pitfall:** Profiling adds a small amount of overhead, so it is disabled in production builds by default. Use it for development and analysis, or opt into a special production build with profiling enabled if needed.[^21_7]

***

### 3. Error Logging and Reporting

Catching errors during development is one thing; understanding errors that happen to real users in production is another.

#### Local Error Handling: Error Boundaries

As covered in Section 9, Error Boundaries are class components that catch rendering errors in their child tree and display a fallback UI instead of crashing the whole app. They are the first line of defense against runtime errors in the UI.[^21_9]

```jsx
// A basic error boundary
componentDidCatch(error, errorInfo) {
  // Log the error to an external service
  logErrorToMyService(error, errorInfo);
}
```


#### Production Error Monitoring: Sentry

For production applications, you need a dedicated error monitoring service. **Sentry** is a popular choice in the React ecosystem that provides comprehensive error tracking and performance monitoring.[^21_10]

**How it works:**

1. **Install:** `npm install @sentry/react`.[^21_11]
2. **Initialize:** You initialize Sentry at the very top of your application's entry point (`index.js` or `main.jsx`) with a unique DSN (Data Source Name) provided by Sentry.[^21_11]
3. **Capture Errors:** Sentry automatically captures unhandled exceptions. You can also wrap your application in Sentry's own Error Boundary to capture rendering errors and display a feedback form to the user.[^21_12]
```jsx
// main.jsx
import * as Sentry from "@sentry/react";

Sentry.init({
  dsn: "YOUR_SENTRY_DSN",
  integrations: [Sentry.browserTracingIntegration()],
  tracesSampleRate: 1.0, // Capture 100% of transactions for performance monitoring
});

// ... then render your app
```

* **Benefit:** Sentry provides a full stack trace, device information, user actions leading up to the error ("breadcrumbs"), and performance metrics, giving you all the context you need to debug production issues quickly.[^21_13]

***

Would you like to continue with Section 21: Folder Structure \& Anti-Patterns?
<span style="display:none">[^21_14][^21_15][^21_16][^21_17][^21_18][^21_19][^21_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^21_1]: https://www.debugbear.com/blog/react-devtools

[^21_2]: https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en

[^21_3]: https://www.freecodecamp.org/news/how-to-use-react-devtools/

[^21_4]: https://reactnative.dev/docs/react-native-devtools

[^21_5]: https://www.reddit.com/r/reactjs/comments/17npptf/how_often_do_you_use_the_react_developer_tools/

[^21_6]: https://deadsimplechat.com/blog/react-profiler/

[^21_7]: https://react.dev/reference/react/Profiler

[^21_8]: https://legacy.reactjs.org/docs/profiler.html

[^21_9]: https://legacy.reactjs.org/docs/error-boundaries.html

[^21_10]: https://sentry.io/for/react/

[^21_11]: https://200oksolutions.com/blog/sentry-error-monitoring-reactjs/

[^21_12]: https://docs.sentry.io/platforms/javascript/guides/react/

[^21_13]: https://innostax.com/sentry-integration-in-react-app-and-streamlining-ci-cd-pipelines/

[^21_14]: https://react.dev/learn/react-developer-tools

[^21_15]: https://www.npmjs.com/package/react-devtools

[^21_16]: https://www.loggly.com/blog/best-practices-for-client-side-logging-and-error-handling-in-react/

[^21_17]: https://blog.bitsrc.io/react-error-handling-and-logging-best-practices-4444c57cd666

[^21_18]: https://www.youtube.com/watch?v=QbSXXXEGA70

[^21_19]: https://www.reddit.com/r/reactjs/comments/158idn0/profiling_react_applications/

[^21_20]: https://docs.sentry.io/platforms/react-native/integrations/


---

# yes

Of course. Here is the revision guide for Section 21.

### Folder Structure \& Anti-Patterns

A well-organized folder structure is crucial for the maintainability and scalability of a React project. While there's no single "correct" way, some established patterns help keep code clean and manageable as a project grows.[^22_1]

***

### Scalable Folder Structures

The best structure often evolves with the project's complexity. A common and highly scalable approach is **feature-based grouping**.[^22_2]

**1. Simple (Grouping by File Type)**

Good for small projects. All components are in one folder, all hooks in another, etc.[^22_3]

```
src/
├── components/
│   ├── Button.js
│   └── UserProfile.js
├── hooks/
│   └── useFetch.js
└── App.js
```

**2. Scalable (Grouping by Feature or Domain)**

Best for medium to large applications. Co-locate all files related to a single feature (components, hooks, styles, tests) inside a dedicated feature folder.[^22_4][^22_5]

* **Analogy:** Instead of organizing a library by book format (hardcover, paperback), you organize it by subject (fiction, history, science). This makes it much easier to find everything related to a specific topic.

```
src/
├── features/
│   ├── authentication/
│   │   ├── components/
│   │   │   ├── LoginForm.js
│   │   │   └── SignupForm.js
│   │   ├── hooks/
│   │   │   └── useAuth.js
│   │   └── index.js
│   └── posts/
│       ├── components/
│       │   ├── PostList.js
│       │   └── PostItem.js
│       └── hooks/
│           └── usePosts.js
├── components/  // For truly shared, reusable UI components
│   ├── Button.js
│   └── Modal.js
└── App.js
```

**Folder Structure Best Practices:**

* **Start Simple, Evolve:** Don't over-engineer your structure at the beginning. Start with a simple model and refactor into a feature-based structure as the application grows.[^22_6]
* **Avoid Deep Nesting:** A good rule of thumb is to avoid nesting folders more than two or three levels deep to keep paths manageable.[^22_4]
* **Shared vs. Feature-Specific:** Create a top-level `components/` or `ui/` directory for components that are genuinely reusable across the entire application (e.g., `Button`, `Input`, `Modal`). Keep components used by only one feature inside that feature's folder.[^22_7]
* **Use Absolute Imports:** Configure path aliases (e.g., `@/components` instead of `../../../components`) in your build tool to avoid long, fragile relative paths.[^22_4]

***

### Common React Anti-Patterns

Anti-patterns are common practices that seem like good solutions but lead to problems down the line. Avoiding them is key to writing clean, maintainable code.[^22_8]


| Anti-Pattern | Problem | Solution |
| :-- | :-- | :-- |
| **Directly Mutating State** | Causes unpredictable behavior and breaks React's rendering lifecycle because React doesn't detect the change[^22_9]. | Always use the `setState` function returned by `useState` or `dispatch` from `useReducer`. |
| **Using Index as `key` for Lists** | Leads to incorrect rendering and state management issues when list items are added, removed, or reordered. | Use a stable, unique identifier from your data (e.g., `item.id`) as the `key`. |
| **Declaring Components Inside Other Components** | The inner component is re-created on every render of the parent, losing its state and causing major performance issues[^22_8]. | Always define components at the top level of a module. |
| **Not Listing All Dependencies in Hooks** | Leads to stale closures where hooks like `useEffect` or `useCallback` use outdated values of props or state, causing subtle and hard-to-find bugs[^22_8]. | Always include every reactive value used inside the hook in its dependency array. Use the `eslint-plugin-react-hooks` to enforce this. |
| **Using `useEffect` for Everything** | Many tasks can be handled more simply. `useEffect` is for synchronization with external systems, not for transforming data or handling simple events. | Derive state directly during rendering, or use event handlers. |


***

### Anti-Pattern Deep Dive: Prop Drilling

**Prop drilling** is the situation where you pass props down through multiple layers of nested components that don't actually need the props, just to get them to a deeply nested child that does.[^22_10]

**Why is it a problem?**

* **Maintenance Nightmare:** Refactoring becomes difficult. If you need to change the prop's name or shape, you have to edit every intermediate component.[^22_11]
* **Reduced Reusability:** Components become tightly coupled to the props they are forced to pass down.[^22_12]
* **Code Clutter:** It makes components harder to read and understand.

**How to Avoid It:**

* **Component Composition:** Often, you can restructure your components to pass JSX as `children` instead of passing data down.

```jsx
// Instead of this:
<Page user={user} avatarSize={avatarSize} />

// Do this:
<Page userSection={<UserAvatar user={user} size={avatarSize} />} />
```

* **React Context:** For global state that many components need (e.g., theme, authenticated user), the Context API is the built-in solution to avoid prop drilling.[^22_11]
* **State Management Libraries:** For complex, app-wide state, libraries like **Zustand** or **Redux** provide a centralized store that any component can subscribe to directly.

***

Would you like to continue with Section 22: Ecosystem Awareness?
<span style="display:none">[^22_13][^22_14][^22_15][^22_16][^22_17][^22_18][^22_19][^22_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^22_1]: https://legacy.reactjs.org/docs/faq-structure.html

[^22_2]: https://profy.dev/article/react-folder-structure

[^22_3]: https://blog.webdevsimplified.com/2022-07/react-folder-structure/

[^22_4]: https://www.robinwieruch.de/react-folder-structure/

[^22_5]: https://www.xenonstack.com/insights/reactjs-project-structure

[^22_6]: https://www.reddit.com/r/reactjs/comments/14zqs61/react_folder_structure/

[^22_7]: https://www.youtube.com/watch?v=_bIJoOriBxA

[^22_8]: https://www.perssondennis.com/articles/react-anti-patterns-and-best-practices-dos-and-donts

[^22_9]: https://www.greatfrontend.com/questions/quiz/what-are-some-react-anti-patterns

[^22_10]: https://www.freecodecamp.org/news/avoid-prop-drilling-in-react/

[^22_11]: https://www.geeksforgeeks.org/reactjs/what-is-prop-drilling-and-how-to-avoid-it/

[^22_12]: https://www.freecodecamp.org/news/prop-drilling-in-react-explained-with-examples/

[^22_13]: https://dev.to/itswillt/folder-structures-in-react-projects-3dp8

[^22_14]: https://www.developerway.com/posts/react-project-structure

[^22_15]: https://dev.to/devland/scalable-and-maintainable-react-project-structure-every-developer-should-use-3om4

[^22_16]: https://www.reddit.com/r/reactjs/comments/182uz8g/when_is_prop_drilling_ok/

[^22_17]: https://maxrozen.com/guidelines-improve-react-app-folder-structure

[^22_18]: https://www.linkedin.com/posts/siddharth-ray-54a5041b_reactjs-redux-frontenddevelopment-activity-7322890945841037314-OIb6

[^22_19]: https://github.com/PacktPublishing/React-Anti-Patterns

[^22_20]: https://www.reddit.com/r/reactjs/comments/1d5ye6y/list_of_antipatterns_in_react_you_should_watch_for/


---

# yes

Of course. This final section provides a high-level overview of the broader React ecosystem, which is crucial for understanding where React fits in the modern web development landscape.

### Ecosystem Awareness

Being a great React developer means not only knowing React itself but also understanding the frameworks, tools, and platforms that surround it.


| Tool / Framework | Category | Core Idea | Best For |
| :-- | :-- | :-- | :-- |
| **Next.js** | Full-Stack Framework | The production standard for building complete React applications with built-in server-side rendering, routing, and API endpoints[^23_1][^23_2]. | SEO-driven websites, e-commerce sites, and complex full-stack applications[^23_3]. |
| **Remix** | Full-Stack Framework | A framework focused on web standards, progressive enhancement, and a superior developer experience through features like nested routing and simplified data loading[^23_4][^23_5]. | Content-rich, form-heavy applications where performance and resilience are critical[^23_6]. |
| **Gatsby** | Static Site Generator | A tool that pulls data from various sources at build time to generate a set of highly optimized, pre-rendered static HTML files[^23_7]. | Blazing-fast marketing sites, blogs, and documentation portals where content doesn't change frequently[^23_8]. |
| **React Native** | Mobile App Framework | A framework for building truly native mobile apps for iOS and Android using a single React codebase[^23_9]. | Developing cross-platform mobile applications without needing to learn Swift or Kotlin[^23_10]. |
| **Expo** | React Native Platform | A framework and set of tools built on top of React Native that simplifies mobile development with a large pre-built SDK, cloud build services, and over-the-air updates[^23_11]. | Rapidly developing and deploying React Native apps, especially for developers coming from a web background[^23_12]. |
| **Vite** | Build Tool | A modern, extremely fast build tool and development server that uses native ES modules to provide instant server start and lightning-fast Hot Module Replacement (HMR)[^23_13][^23_14]. | Starting new React projects that prioritize development speed and a simple configuration[^23_13]. |
| **Astro** | Static Site Generator | A modern "content-first" framework that can use components from any UI library (including React) but ships zero JavaScript to the client by default, only "hydrating" interactive components[^23_15]. | Building high-performance, content-focused websites like blogs and portfolios with excellent load times[^23_16]. |


***

This concludes the quick revision guide. I hope this structured overview helps with your interview preparation! Let me know if you'd like to revisit or dive deeper into any specific section. Good luck
<span style="display:none">[^23_17][^23_18][^23_19][^23_20]</span>

```
<div style="text-align: center">⁂</div>
```

[^23_1]: https://nextjs.org/learn

[^23_2]: https://welearncode.com/beginners-guide-nextjs/

[^23_3]: https://www.tutorialspoint.com/nextjs/index.htm

[^23_4]: https://www.contentful.com/blog/remix-vs-nextjs/

[^23_5]: https://remix.run

[^23_6]: https://www.geeksforgeeks.org/javascript/remix-introduction-installation/

[^23_7]: https://github.com/gatsbyjs/gatsby

[^23_8]: https://stackoverflow.com/questions/65416545/how-does-react-work-on-gatsby-statically-generated

[^23_9]: https://www.geeksforgeeks.org/react-native/react-native-tutorial/

[^23_10]: https://reactnative.dev/docs/tutorial

[^23_11]: https://reactnative.dev/docs/environment-setup

[^23_12]: https://www.youtube.com/watch?v=J2j1yk-34OY

[^23_13]: https://codeparrot.ai/blogs/a-beginners-guide-to-using-vite-react

[^23_14]: https://vite.dev/guide/

[^23_15]: https://www.telerik.com/blogs/integrating-react-astro

[^23_16]: https://www.dhiwise.com/post/astro-vs-react-comparing-their-roles-in-web-development

[^23_17]: https://www.geeksforgeeks.org/nextjs/nextjs-tutorial/

[^23_18]: https://www.youtube.com/watch?v=ZVnjOPwW4ZA

[^23_19]: https://nextjs.org/learn/pages-router

[^23_20]: https://nextjs.org/docs

