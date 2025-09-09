### FrontEnd General Interview Questions and Answers

## 1. Core Frontend Fundamentals

- HTML5 semantics, forms, accessibility (ARIA, alt, roles).
- CSS3: box model, positioning, flexbox, grid, responsive design.
- JavaScript ES6+: closures, promises, async/await, event loop, hoisting, var/let/const.

## 2. React.js & Ecosystem

- JSX, components (functional/class), props, state.
- Hooks (useState, useEffect, useMemo, useCallback, custom hooks).
- State management (Context API, Redux, Zustand, etc.).
- Virtual DOM & reconciliation.
- Controlled vs uncontrolled components.
- Performance optimization (memoization, lazy loading, code splitting).
- Error boundaries, debugging, React DevTools.

## 3. Modern Frontend Engineering

- Build tools: Webpack, Vite, Rollup.
- ESLint, Prettier, and code quality practices.
- Large-scale performance strategies (bundle splitting, tree shaking, caching).

#### How does CSS Flexbox differ from Grid?

**Answer:**

- Flexbox is 1D (row or column) — great for alignment/distribution.
- Grid is 2D (rows + columns) — great for full page layouts.

Example:

- Navbars → Flexbox
- Dashboard layouts → Grid

#### Difference between relative, absolute, fixed, and sticky positioning?

**Answer:**

- relative: relative to itself.
- absolute: relative to nearest positioned ancestor.
- fixed: relative to viewport (stays on scroll).
- sticky: hybrid; scrolls until threshold, then sticks.

#### What is `useState` and `useEffect` in React?

**Answer:**

- `useState` is a Hook that lets you add React state to function components. It returns an array with two elements: the current state value and a function that lets you update it.

  ```jsx
  const [count, setCount] = useState(0);
  ```

- `useEffect` is a Hook that lets you perform side effects in function components. It runs after the render and can be used for fetching data, directly updating the DOM, and setting up subscriptions.

  ```jsx
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]); // Only re-run the effect if count changes
  ```

#### What are all the hooks available in React?

**Answer:**

React provides several built-in hooks, including:

- `useState`: Manages state in a functional component.
- `useEffect`: Performs side effects in functional components.
- `useContext`: Accesses the context in a functional component.
- `useReducer`: Manages complex state logic with reducers.
- `useCallback`: Returns a memoized callback function.
- `useMemo`: Returns a memoized value.
- `useRef`: Accesses and interacts with DOM elements or persistent values.
- `useLayoutEffect`: Similar to `useEffect`, but it fires synchronously after all DOM mutations.
- `useDebugValue`: Displays a label for custom hooks in React DevTools.
- `useImperativeHandle`: Customizes the instance value that is exposed to parent components when using `ref`.

#### What is the Virtual DOM (VDOM)?

**Answer:**

The Virtual DOM (VDOM) is a lightweight JavaScript representation of the actual DOM. It is a concept where a virtual representation of the UI is kept in memory and synced with the real DOM by a library such as ReactDOM. This process is known as reconciliation. The Virtual DOM improves performance by minimizing direct manipulations of the DOM and applying updates efficiently.

#### What is Redux?

**Answer:**

Redux is a state management library for JavaScript applications, commonly used with React. It helps manage the state of an application in a predictable way using a single source of truth (a store). Redux principles include:

- **Single source of truth:** The state of the whole application is stored in an object tree within a single store.
- **State is read-only:** The only way to change the state is to emit an action, an object describing what happened.
- **Changes are made with pure functions:** To specify how the state tree is transformed by actions, you write pure reducers.

#### What is Formik?

**Answer:**

Formik is a popular library used in React for handling forms. It provides a set of tools to manage form state, validation, and submission. Formik aims to reduce the boilerplate code around forms, making them easier to work with and more maintainable.

```jsx
import { useFormik } from "formik";

const MyForm = () => {
  const formik = useFormik({
    initialValues: {
      email: "",
    },
    onSubmit: (values) => {
      console.log("Form data", values);
    },
  });

  return (
    <form onSubmit={formik.handleSubmit}>
      <input
        id="email"
        name="email"
        type="email"
        onChange={formik.handleChange}
        value={formik.values.email}
      />
      <button type="submit">Submit</button>
    </form>
  );
};
```

#### What is Axios?

**Answer:**

Axios is a promise-based HTTP client for the browser and Node.js. It makes it easy to send asynchronous HTTP requests to REST endpoints and perform CRUD operations. Axios supports automatic transformation of JSON data, interception of requests and responses, and more.

```jsx
import axios from "axios";

axios
  .get("/user?ID=12345")
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error fetching data", error);
  });
```

#### How to set headers in Axios?

**Answer:**

Headers can be set in Axios requests by passing a `headers` object in the request configuration. Here is an example of how to set headers in a GET request:

```jsx
import axios from "axios";

axios
  .get("/user?ID=12345", {
    headers: {
      Authorization: "Bearer token",
      "Content-Type": "application/json",
    },
  })
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error fetching data", error);
  });
```

In a POST request, you can set headers similarly:

```jsx
axios
  .post(
    "/user",
    {
      firstName: "Fred",
      lastName: "Flintstone",
    },
    {
      headers: {
        Authorization: "Bearer token",
        "Content-Type": "application/json",
      },
    }
  )
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error("Error posting data", error);
  });
```

## How to Create a Custom Hook in React

### Steps to Create a Custom Hook

1. **Identify the Reusable Logic**: Determine the logic you want to reuse across multiple components.
2. **Create the Custom Hook**: Create a new function that encapsulates this logic. The function should start with "use".
3. **Use the Custom Hook in Components**: Call your custom hook inside a function component just like you would call a built-in hook.

### Custom Hook Example: `useCounter`

Let's create a custom hook called `useCounter` that manages a counter state. This hook will provide functionality to increment, decrement, and reset the counter.

### Creating the Custom Hook

Create a file named `useCounter.js` and add the following code:

```javascript
import { useState } from "react";

// Custom Hook
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(initialValue);

  return { count, increment, decrement, reset };
}

export default useCounter;
```

#### Explanation:

- `useCounter` is a custom hook that takes an `initialValue` as an argument and initializes the counter state to this value.
- The hook uses the `useState` hook to manage the counter state.
- It defines three functions: `increment`, `decrement`, and `reset` to update the state.
- The hook returns an object containing the current `count` and the three functions to manipulate the count.

### Using the Custom Hook in a Component

Now, let's use the `useCounter` hook in a functional component.

Create a file named `CounterComponent.js` and add the following code:

```javascript
import React from "react";
import useCounter from "./useCounter";

function CounterComponent() {
  const { count, increment, decrement, reset } = useCounter(10);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

export default CounterComponent;
```

#### Explanation:

- `CounterComponent` is a functional component that uses the `useCounter` hook.
- It calls the `useCounter` hook with an initial value of `10`.
- The hook returns the current `count` and the `increment`, `decrement`, and `reset` functions.
- The component renders the current count and three buttons to increment, decrement, and reset the count using the functions provided by the hook.

### Putting It All Together

Here is how the custom hook and component would look together in a simple React application.

#### `useCounter.js`

```javascript
import { useState } from "react";

// Custom Hook
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(initialValue);

  return { count, increment, decrement, reset };
}

export default useCounter;
```

#### `CounterComponent.js`

```javascript
import React from "react";
import useCounter from "./useCounter";

function CounterComponent() {
  const { count, increment, decrement, reset } = useCounter(10);

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

export default CounterComponent;
```

#### `App.js`

```javascript
import React from "react";
import CounterComponent from "./CounterComponent";

function App() {
  return (
    <div className="App">
      <CounterComponent />
    </div>
  );
}

export default App;
```

#### Explanation:

- `useCounter.js` defines the custom hook.
- `CounterComponent.js` uses the custom hook to manage the counter state and provides a UI to interact with it.
- `App.js` is the main application component that renders `CounterComponent`.

---

Certainly! Below is a list of commonly asked React interview questions for a senior UI developer, along with their answers and example code, formatted in Markdown.

---

# React Interview Questions and Answers

## 1. What are the key features of React?

**Answer:**
React is a popular JavaScript library for building user interfaces. Its key features include:

- **Component-Based Architecture:** Building encapsulated components that manage their own state and compose them to make complex UIs.
- **Virtual DOM:** React creates a virtual DOM and updates it efficiently, minimizing direct DOM manipulation.
- **One-Way Data Binding:** Data flows in a single direction, making it easier to debug and understand.
- **JSX:** JavaScript syntax extension that allows mixing HTML with JavaScript.

## 2. Explain the difference between functional and class components.

**Answer:**

- **Class Components:** These are ES6 classes that extend from `React.Component` and must have a `render` method returning JSX. They can hold and manage local state and have lifecycle methods.

  ```jsx
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);
      this.state = { count: 0 };
    }

    render() {
      return (
        <div>
          <p>Count: {this.state.count}</p>
          <button
            onClick={() => this.setState({ count: this.state.count + 1 })}
          >
            Increment
          </button>
        </div>
      );
    }
  }
  ```

- **Functional Components:** These are simpler and are just functions that receive props as an argument and return JSX. They can use hooks to manage state and lifecycle methods.

  ```jsx
  function MyComponent() {
    const [count, setCount] = React.useState(0);

    return (
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
      </div>
    );
  }
  ```

## 3. What are hooks in React?

**Answer:**
Hooks are functions that let you "hook into" React state and lifecycle features from functional components. Some commonly used hooks are:

- `useState`: Allows you to add state to functional components.
- `useEffect`: Allows you to perform side effects in function components.
- `useContext`: Lets you subscribe to React context without introducing nesting.

Example using `useState` and `useEffect`:

```jsx
import React, { useState, useEffect } from "react";

function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

## 4. What is the context API?

**Answer:**
The Context API is a way to pass data through the component tree without having to pass props down manually at every level. It is often used for theming, user authentication, and language settings.

Example:

```jsx
import React, { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return (
    <button style={{ background: theme === "dark" ? "#333" : "#FFF" }}>
      I am styled by theme context!
    </button>
  );
}
```

## 5. How do you handle forms in React?

**Answer:**
Handling forms in React involves managing form state, handling user inputs, and submitting the form. Controlled components are commonly used for this purpose.

Example:

```jsx
import React, { useState } from "react";

function MyForm() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Name: ${name}, Email: ${email}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input
          type="text"
          value={name}
          onChange={(e) => setName(e.target.value)}
        />
      </label>
      <br />
      <label>
        Email:
        <input
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
      </label>
      <br />
      <button type="submit">Submit</button>
    </form>
  );
}
```

## 6. Explain the concept of "lifting state up" in React.

**Answer:**
Lifting state up is a common pattern in React where state is moved up to the closest common ancestor of components that need to share that state. This ensures that state is managed in one place and can be passed down to child components via props.

Example:

```jsx
function Parent() {
  const [sharedState, setSharedState] = useState(0);

  return (
    <div>
      <ChildA sharedState={sharedState} setSharedState={setSharedState} />
      <ChildB sharedState={sharedState} />
    </div>
  );
}

function ChildA({ sharedState, setSharedState }) {
  return (
    <button onClick={() => setSharedState(sharedState + 1)}>
      Increment from ChildA
    </button>
  );
}

function ChildB({ sharedState }) {
  return <p>Shared State: {sharedState}</p>;
}
```

## 7. What are React fragments and why are they useful?

**Answer:**
React fragments allow you to group multiple elements without adding extra nodes to the DOM. They are useful for returning multiple elements from a component without adding unnecessary div wrappers.

Example:

```jsx
import React from "react";

function FragmentExample() {
  return (
    <>
      <p>First element</p>
      <p>Second element</p>
    </>
  );
}
```

## 8. How do you optimize performance in a React application?

**Answer:**
Performance optimization in React can be achieved through several techniques:

- **Memoization:** Using `React.memo` to prevent unnecessary re-renders.
- **useCallback and useMemo Hooks:** To memoize functions and values respectively.
- **Code Splitting:** Using dynamic `import()` to split code into smaller bundles.
- **Virtualization:** Rendering only the visible part of a large list using libraries like `react-window` or `react-virtualized`.

Example using `React.memo` and `useCallback`:

```jsx
import React, { useState, useCallback } from "react";

const Child = React.memo(({ onClick }) => {
  console.log("Child rendered");
  return <button onClick={onClick}>Click me</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <Child onClick={handleClick} />
    </div>
  );
}
```

## 9. What are higher-order components (HOC)?

**Answer:**
Higher-order components (HOC) are functions that take a component and return a new component with additional props or functionality. They are used to reuse component logic.

Example:

```jsx
import React from "react";

function withLogging(WrappedComponent) {
  return class extends React.Component {
    componentDidMount() {
      console.log("Component mounted");
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
}

function MyComponent(props) {
  return <div>My Component {props.name}</div>;
}

const MyComponentWithLogging = withLogging(MyComponent);
```

## 10. How does error handling work in React?

**Answer:**
Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the whole component tree. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.

Example:

```jsx
import React from "react";

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    console.error("Error:", error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}

function MyComponent() {
  throw new Error("Test error");
  return <div>My Component</div>;
}

function App() {
  return (
    <ErrorBoundary>
      <MyComponent />
    </ErrorBoundary>
  );
}
```

---
