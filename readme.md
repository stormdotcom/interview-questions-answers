# JavaScript Interview Questions & Answers

## Table of Contents

1. [Debounce Function](#1-debounce-function)
2. [Throttle Function](#2-throttle-function)
3. [Currying](#3-currying)
4. [Deep Flatten Array](#4-deep-flatten-array)
5. [Pipe Function](#5-pipe-function)
6. [Auto-retry Promises](#6-auto-retry-promises)
7. [Defer & Async Script Attributes](#7-defer--async-script-attributes)
8. [Async/Await, Event Loop, Callback Functions](#8-asyncawait-event-loop-callback-functions)
9. [Promises](#9-promises)
10. [Array Methods](#10-array-methods)
11. [Splice vs Slice](#11-splice-vs-slice)
12. [Prototypes](#12-prototypes)
13. [call, apply, bind](#13-call-apply-bind)
14. [Object Methods](#14-object-methods)
15. [Convert Array to String](#15-convert-array-to-string)
16. [ES6 Features](#16-es6-features)
17. [Modules](#17-modules)
18. [Web APIs](#18-web-apis)
19. [JavaScript Concepts](#19-javascript-concepts)
20. [Worker Threads](#20-worker-threads)
21. [Full-Stack Interview Questions (Extra)](FullStack_Interview_Questions_Extra.md)
22. [JavaScript Output Questions](javascript.md)

---

### 1. Debounce Function

**Question:** Implement a debounce function that delays the processing of the input function until after a specified wait time has elapsed since the last time the debounce function was invoked.

```javascript
function debounce(func, wait) {
  let timeout;
  return function (...args) {
    const context = this;
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(context, args), wait);
  };
}

// Usage
const debouncedFunction = debounce(() => console.log("Debounced!"), 300);
window.addEventListener("resize", debouncedFunction);
```

---

### 2. Throttle Function

**Question:** Implement a throttle function that ensures a function is called at most once in a specified time interval.

```javascript
function throttle(func, limit) {
  let lastFunc;
  let lastRan;
  return function (...args) {
    const context = this;
    if (!lastRan) {
      func.apply(context, args);
      lastRan = Date.now();
    } else {
      clearTimeout(lastFunc);
      lastFunc = setTimeout(function () {
        if (Date.now() - lastRan >= limit) {
          func.apply(context, args);
          lastRan = Date.now();
        }
      }, limit - (Date.now() - lastRan));
    }
  };
}
```

---

### 3. Currying

**Question:** Implement a function currying method that transforms a function with multiple arguments into a series of functions each with a single argument.

```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    } else {
      return function (...args2) {
        return curried.apply(this, args.concat(args2));
      };
    }
  };
}
```

---

### 4. Deep Flatten Array

**Question:** Write a function to deeply flatten an array of arrays.

```javascript
function deepFlatten(arr) {
  return arr.reduce(
    (acc, val) =>
      Array.isArray(val) ? acc.concat(deepFlatten(val)) : acc.concat(val),
    []
  );
}
```

---

### 5. Pipe Function

**Question:** Implement a function `pipe` that performs left-to-right function composition.

```javascript
function pipe(...functions) {
  return function (input) {
    return functions.reduce((acc, fn) => fn(acc), input);
  };
}
```

---

### 6. Auto-retry Promises

**Question:** Implement a function that retries a promise-returning function a specified number of times before rejecting.

```javascript
function autoRetry(promiseFn, retries) {
  return function (...args) {
    let attempts = 0;
    function execute() {
      return promiseFn(...args).catch((err) => {
        if (attempts < retries) {
          attempts++;
          return execute();
        } else {
          return Promise.reject(err);
        }
      });
    }
    return execute();
  };
}
```

---

### 7. Defer & Async Script Attributes

- **defer**: Downloads script in background, executes after HTML is parsed.
- **async**: Downloads script in background, executes as soon as downloaded.

---

### 8. Async/Await, Event Loop, Callback Functions

- **Async/Await**: Syntactic sugar over promises for cleaner async code.
- **Event Loop**: Handles non-blocking operations, processes message queue.
- **Callback Functions**: Functions passed as arguments to be executed later.

---

### 9. Promises

A promise represents the eventual completion or failure of an async operation.

---

### 10. Array Methods

- **forEach**: Executes a function for each array element.
- **map**: Creates a new array with results of calling a function on every element.
- **reduce**: Reduces array to a single value.
- **filter**: Creates a new array with elements that pass a test.

---

### 11. Splice vs Slice

- **splice**: Changes array by removing/replacing/adding elements.
- **slice**: Returns a shallow copy of a portion of an array.

---

### 12. Prototypes

Prototypes allow objects to inherit features from one another.

---

### 13. call, apply, bind

# JavaScript: call, apply, and bind – Interview Questions & Answers

## 1. What is the `call()` method in JavaScript? Give an example.

**Answer:**
The `call()` method allows you to call a function immediately, setting the value of `this` inside the function and passing arguments individually.

**Example:**

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

const person = { name: "Alice" };
greet.call(person, "Hello", "!"); // Output: Hello, Alice!
```

## 2. What is the `apply()` method in JavaScript? Give an example.

**Answer:**
The `apply()` method is very similar to `call()`, but you pass the function arguments as an array instead of individually.

**Example:**

```javascript
function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

const person = { name: "Bob" };
greet.apply(person, ["Hi", "?"]); // Output: Hi, Bob?
```

## 3. What is the difference between `call()` and `apply()`?

**Answer:**

- Both methods call the function immediately and allow you to set `this`.
- The key difference is how arguments are passed:
  - `call(thisArg, arg1, arg2, ...)`: Passes arguments individually.
  - `apply(thisArg, [arg1, arg2, ...])`: Passes arguments as an array.

## 4. What does the `bind()` method do in JavaScript? Give an example.

**Answer:**
The `bind()` method returns a new function with a specified value of `this` and, optionally, preset arguments. It does **not** call the function immediately.

**Example:**

```javascript
function greet(greeting) {
  console.log(greeting + ", " + this.name);
}

const person = { name: "Charlie" };
const greetCharlie = greet.bind(person, "Hey");
greetCharlie(); // Output: Hey, Charlie
```

## 5. What is the main difference between `call`/`apply` and `bind`?

**Answer:**

- `call()` and `apply()` invoke the function immediately with the specified context.
- `bind()` creates a new function that, when called, has its `this` keyword set to the provided value, but does not invoke the function immediately.

## 6. When would you use `bind` instead of `call`/`apply`?

**Answer:**
Use `bind` when you need to create a function with a fixed `this` value that can be called later, such as event handlers or callbacks, rather than calling the function immediately.

## 7. Summary Table

| Method  | Calls function immediately? | How are arguments passed? | Returns new function? |
| ------- | --------------------------- | ------------------------- | --------------------- |
| `call`  | Yes                         | Individually              | No                    |
| `apply` | Yes                         | As an array               | No                    |
| `bind`  | No                          | Individually (pre-set)    | Yes                   |

Feel free to use these for quick interview prep or as reference notes!

---

### 14. Object Methods

- **Object.keys()**: Returns array of property names.
- **Object.values()**: Returns array of property values.
- **Object.entries()**: Returns array of [key, value] pairs.

---

### 15. Convert Array to String

- `toString()`, `join()`, `JSON.stringify()`

---

### 16. ES6 Features

- **Arrow Functions**
- **Spread Operator**
- **Destructuring**

---

### 17. Modules

- **Export/Import**: Use `export` and `import` to share code between files.

---

### 18. Web APIs

- **Local Storage**
- **Geolocation**
- **Session Storage**
- **Intersection Observer**
- **WebSocket**

---

### 19. JavaScript Concepts

- **Workflow**: Parsing, execution context, event handling.
- **Hoisting**: Declarations moved to top of scope.
- **Closure**: Functions retain access to their lexical scope.
- **Event Delegation**: Handle events at a parent level.
- **Event Loop**: Manages call stack and message queue.
- **Stack/Queue**: LIFO/FIFO data structures.
- **Lexical Context**: Scope where variables/functions are defined.
- **First-Class Functions**: Functions as variables, arguments, return values.
- **Execution Context**: Global, function, eval contexts.
- **Async Working**: Callbacks, promises, async/await.
- **Copy by Value**: Shallow/deep copy techniques.
- **Arrow Function `this`**: Inherits from lexical scope.

---

### 20. Worker Threads

**Question:** What are Worker Threads in JavaScript and when should you use them?

**Answer:**

Worker Threads allow JavaScript to run code in parallel on multiple threads, which is especially useful for CPU-intensive tasks. In browsers, this is achieved with Web Workers; in Node.js, with the `worker_threads` module. Worker threads do not share scope with the main thread and communicate via message passing.

**Example (Node.js):**

```javascript
const { Worker, isMainThread, parentPort } = require("worker_threads");

if (isMainThread) {
  const worker = new Worker(__filename);
  worker.on("message", (msg) => console.log("From worker:", msg));
  worker.postMessage("Hello from main thread");
} else {
  parentPort.on("message", (msg) => {
    parentPort.postMessage("Received: " + msg);
  });
}
```

**When to use:**

- Heavy computations (e.g., image processing, data parsing)
- Avoiding blocking the main event loop

---

# End of Questions

### **Understanding `Promise` Constructor and `then` Method**

```javascript
const p = new Promise((resolve, reject) => {
  console.log("Promise started");
  resolve("Resolved value");
});

p.then((res) => {
  console.log(res);
});

console.log("Promise created");
```

**Question:** What will be the output of the above code, and in what order?

#### **Answer:**

The output will be:

```
Promise started
Promise created
Resolved value
```

**Explanation:**

- **"Promise started"** is printed first when the `Promise` constructor is executed.
- **"Promise created"** is printed next, right after the `Promise` is created.
- The `then` method is added to the microtask queue. Once the synchronous code is finished, **"Resolved value"** is logged.

---

### **Combining `async/await` with Multiple Promises**

```javascript
async function asyncTask1() {
  console.log("Task 1 started");
  await new Promise((resolve) => setTimeout(resolve, 2000));
  console.log("Task 1 completed");
}

async function asyncTask2() {
  console.log("Task 2 started");
  await new Promise((resolve) => setTimeout(resolve, 1000));
  console.log("Task 2 completed");
}

async function main() {
  console.log("Main started");
  await asyncTask1();
  await asyncTask2();
  console.log("Main completed");
}

main();
```

**Question:** What will be the output of this code, and how long will it take to execute completely?

#### **Answer:**

The output will be:

```
Main started
Task 1 started
Task 1 completed
Task 2 started
Task 2 completed
Main completed
```

**Explanation:**

- **"Main started"** is printed first.
- **`asyncTask1`** starts and waits for 2 seconds.
- After 2 seconds, **"Task 1 completed"** is printed.
- **`asyncTask2`** starts and waits for 1 second.
- After 1 second, **"Task 2 completed"** is printed.
- Finally, **"Main completed"** is printed.
- Total time: 2 seconds (for `asyncTask1`) + 1 second (for `asyncTask2`) = **3 seconds**.

---

### **Mixing `setTimeout` and `Promise` Chaining**

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve()
  .then(() => {
    console.log("Promise 1");
  })
  .then(() => {
    console.log("Promise 2");
  });

console.log("End");
```

**Question:** What is the output of the above code and why?

#### **Answer:**

The output will be:

```
Start
End
Promise 1
Promise 2
Timeout
```

**Explanation:**

- **"Start"** is logged first.
- The `setTimeout` callback is added to the macrotask queue.
- The first `Promise` is resolved immediately and **"Promise 1"** is added to the microtask queue.
- **"End"** is logged after the synchronous code completes.
- Microtasks are processed next, so **"Promise 1"** and **"Promise 2"** are logged.
- Finally, the `setTimeout` callback is executed, logging **"Timeout"**.

These types of questions help test the understanding of JavaScript's asynchronous behavior, the event loop, the microtask vs. macrotask queue, and the correct use of `Promises` and `async/await`.

function sayHello() {
setTimeout(() => {
return "Hello";
}, 100);
}

console.log(sayHello());
