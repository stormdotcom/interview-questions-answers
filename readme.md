### Frequently Asked JavaScript Interview Questions

### [React Interview Questions](./ReactJS.md)

### [System Design - FrontEnd](./HLD_FE/FE.md)

### [Problem Solving Questions ](./Problems.md)

### [NextJS Interview Questions ](./NextJS.md)

### [NodeJS Interview Questions ](./NodeJS.md)

### [AWS S3 ](./AWS-S3.md)

### [AWS-Lambda ](./AWS-Lambda.md)

#### 1. Implement Debounce

**Question:**
Implement a debounce function that delays the processing of the input function until after a specified wait time has elapsed since the last time the debounce function was invoked.

**Code:**

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

#### 2. Implement Throttle

**Question:**
Implement a throttle function that ensures a function is called at most once in a specified time interval.

**Code:**

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

// Usage
const throttledFunction = throttle(() => console.log("Throttled!"), 1000);
window.addEventListener("resize", throttledFunction);
```

#### 3. Implement Currying

**Question:**
Implement a function currying method that transforms a function with multiple arguments into a series of functions each with a single argument.

**Code:**

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

// Usage
function add(a, b, c) {
  return a + b + c;
}

const curriedAdd = curry(add);
console.log(curriedAdd(1)(2)(3)); // 6
console.log(curriedAdd(1, 2)(3)); // 6
```

#### 4. Deep Flatten I

**Question:**
Write a function to deeply flatten an array of arrays.

**Code:**

```javascript
function deepFlatten(arr) {
  return arr.reduce(
    (acc, val) =>
      Array.isArray(val) ? acc.concat(deepFlatten(val)) : acc.concat(val),
    []
  );
}

// Usage
const nestedArray = [1, [2, [3, 4], 5], 6];
console.log(deepFlatten(nestedArray)); // [1, 2, 3, 4, 5, 6]
```

#### 5. Implement a Pipe Method

**Question:**
Implement a function `pipe` that performs left-to-right function composition.

**Code:**

```javascript
function pipe(...functions) {
  return function (input) {
    return functions.reduce((acc, fn) => fn(acc), input);
  };
}

// Usage
const add = (x) => x + 1;
const multiply = (x) => x * 2;
const addThenMultiply = pipe(add, multiply);

console.log(addThenMultiply(5)); // 12
```

#### 6. Implement Auto-retry Promises

**Question:**
Implement a function that retries a promise-returning function a specified number of times before rejecting.

**Code:**

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

// Usage
const unreliableFetch = () =>
  new Promise((resolve, reject) =>
    Math.random() > 0.5 ? resolve("Success") : reject("Failed")
  );

const fetchWithRetry = autoRetry(unreliableFetch, 3);
fetchWithRetry().then(console.log).catch(console.error);
```

Sure, here's a detailed answer to each of the topics in Markdown format:

---

#### 7. Defer & Async Attributes of Script Tag

### Defer

The `defer` attribute tells the browser to download the script in the background while the HTML document is still being parsed. The script is executed after the document has been completely parsed.

```html
<script src="script.js" defer></script>
```

#### 8. Async

The `async` attribute also downloads the script in the background, but the script is executed as soon as it is downloaded, without waiting for the HTML parsing to complete.

```html
<script src="script.js" async></script>
```

## Async / Await, Event Loops, Callback Functions

### Async / Await

`async` and `await` are syntactic sugar over promises, providing a cleaner and more intuitive way to work with asynchronous code.

```javascript
async function fetchData() {
  let response = await fetch("https://api.example.com/data");
  let data = await response.json();
  console.log(data);
}
```

#### 9. Async Event Loops

The event loop is a mechanism that allows JavaScript to perform non-blocking operations by offloading operations to the system kernel whenever possible.

#### 10. Callback Functions

A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("Data received");
  }, 1000);
}

fetchData((message) => {
  console.log(message);
});
```

#### 11. Promises

A promise is an object representing the eventual completion or failure of an asynchronous operation.

```javascript
let promise = new Promise((resolve, reject) => {
  let success = true;
  if (success) {
    resolve("Operation succeeded");
  } else {
    reject("Operation failed");
  }
});

promise
  .then((message) => {
    console.log(message);
  })
  .catch((error) => {
    console.error(error);
  });
```

#### 12. Array Methods

### forEach

Executes a provided function once for each array element.

```javascript
[1, 2, 3].forEach((num) => console.log(num));
```

### map

Creates a new array populated with the results of calling a provided function on every element in the calling array.

```javascript
let doubled = [1, 2, 3].map((num) => num * 2);
console.log(doubled); // [2, 4, 6]
```

### reduce

Executes a reducer function on each element of the array, resulting in a single output value.

```javascript
let sum = [1, 2, 3].reduce((acc, num) => acc + num, 0);
console.log(sum); // 6
```

### filter

Creates a new array with all elements that pass the test implemented by the provided function.

```javascript
let evens = [1, 2, 3, 4].filter((num) => num % 2 === 0);
console.log(evens); // [2, 4]
```

#### 13.Splice & Slice Difference

### Splice

Changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.

```javascript
let array = [1, 2, 3, 4, 5];
array.splice(2, 1, 6); // From index 2, remove 1 element and add 6
console.log(array); // [1, 2, 6, 4, 5]
```

### Slice

Returns a shallow copy of a portion of an array into a new array object selected from `start` to `end` (end not included).

```javascript
let array = [1, 2, 3, 4, 5];
let newArray = array.slice(1, 3);
console.log(newArray); // [2, 3]
```

#### 13.Prototype

Prototypes are the mechanism by which JavaScript objects inherit features from one another.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log(`Hello, my name is ${this.name}`);
};

let john = new Person("John");
john.greet(); // Hello, my name is John
```

#### 14. Difference Between call, bind, apply

### call

Calls a function with a given `this` value and arguments provided individually.

```javascript
function greet(greeting) {
  console.log(`${greeting}, my name is ${this.name}`);
}

let person = { name: "John" };
greet.call(person, "Hello"); // Hello, my name is John
```

### apply

Calls a function with a given `this` value and arguments provided as an array.

```javascript
greet.apply(person, ["Hi"]); // Hi, my name is John
```

### bind

Creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments.

```javascript
let greetJohn = greet.bind(person, "Hey");
greetJohn(); // Hey, my name is John
```

#### 15.Object Methods

### Object.keys()

Returns an array of a given object's own enumerable property names.

```javascript
let obj = { a: 1, b: 2, c: 3 };
console.log(Object.keys(obj)); // ["a", "b", "c"]
```

### Object.values()

Returns an array of a given object's own enumerable property values.

```javascript
console.log(Object.values(obj)); // [1, 2, 3]
```

### Object.entries()

Returns an array of a given object's own enumerable property [key, value] pairs.

```javascript
console.log(Object.entries(obj)); // [["a", 1], ["b", 2], ["c", 3]]
```

#### 16. Convert Array to Strings

Convert an array to a string using `toString()`, `join()`, or `JSON.stringify()`.

```javascript
let array = [1, 2, 3, 4, 5];

let str1 = array.toString();
console.log(str1); // "1,2,3,4,5"

let str2 = array.join("-");
console.log(str2); // "1-2-3-4-5"

let str3 = JSON.stringify(array);
console.log(str3); // "[1,2,3,4,5]"
```

#### MISC

## ES6 Features

### Arrow Functions

Provides a shorter syntax for writing function expressions.

```javascript
let add = (a, b) => a + b;
console.log(add(2, 3)); // 5
```

### Spread Operator

Allows an iterable such as an array expression to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected.

```javascript
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];
console.log(arr2); // [1, 2, 3, 4, 5]
```

### Destructuring

A convenient way of extracting multiple values from data stored in objects and arrays.

```javascript
let obj = { a: 1, b: 2, c: 3 };
let { a, b, c } = obj;
console.log(a, b, c); // 1, 2, 3
```

## Modules

ES6 modules allow you to export and import code between files.

### Exporting

```javascript
// module.js
export const name = "John";
export function greet() {
  console.log("Hello");
}
```

### Importing

```javascript
// main.js
import { name, greet } from "./module.js";
console.log(name); // John
greet(); // Hello
```

## JS Debugging

Debug JavaScript using browser developer tools.

- **Console**: Log messages using `console.log()`, `console.error()`, etc.
- **Breakpoints**: Set breakpoints in your code to pause execution and inspect variables.
- **Step Through Code**: Step through your code line by line to see how it executes.

## Web APIs

### Local Storage

Allows you to save key/value pairs in a web browser with no expiration date.

```javascript
localStorage.setItem("name", "John");
console.log(localStorage.getItem("name")); // John
```

### Geolocation

Provides the ability to retrieve the geographic location of the user.

```javascript
navigator.geolocation.getCurrentPosition((position) => {
  console.log(position.coords.latitude, position.coords.longitude);
});
```

### Session Storage

Similar to local storage, but the data is cleared when the page session ends.

```javascript
sessionStorage.setItem("name", "John");
console.log(sessionStorage.getItem("name")); // John
```

### Intersection Observer

Provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.

```javascript
let observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      console.log("Element is in view");
    }
  });
});

observer.observe(document.querySelector("#target"));
```

### WebSocket

Provides a way to open a persistent connection between the client and the server and communicate with messages.

```javascript
let socket = new WebSocket("ws://example.com/socket");

socket.onopen = () => {
  console.log("Connection opened");
  socket.send("Hello Server");
};

socket.onmessage = (event) => {
  console.log("Message from server ", event.data);
};
```

# JavaScript Concepts

## Workflow of JavaScript

**What is the workflow of JavaScript?**

JavaScript executes code in a single-threaded, non-blocking, event-driven environment. The typical workflow includes:

- **Parsing and Compilation:** JavaScript code is parsed and compiled into machine code by the JavaScript engine.
- **Execution Context Creation:** For each function or block of code, an execution context is created, which includes the scope chain, `this` context, and local variables.
- **Execution:** Code is executed within the created execution context, including synchronous code execution and handling asynchronous operations using callbacks, promises, or async/await.
- **Event Handling:** Event listeners are attached to elements, and when events occur, they are processed by the event loop.

## Hoisting

**What is hoisting in JavaScript?**

Hoisting is a JavaScript behavior where variable and function declarations are moved to the top of their containing scope during the compilation phase. This means you can use variables and functions before they are declared in the code.

- **Variables:** Only the declaration is hoisted, not the initialization. Accessing a variable before its initialization will result in `undefined`.

  ```javascript
  console.log(x); // undefined
  var x = 5;
  ```

- **Functions:** Function declarations are fully hoisted, so you can call a function before its declaration.
  ```javascript
  greet(); // Outputs 'Hello!'
  function greet() {
    console.log("Hello!");
  }
  ```

## Closure

**What is a closure?**

A closure is a function that retains access to its lexical scope even after the function has finished executing. Closures allow functions to remember the environment in which they were created.

Example:

```javascript
function createCounter() {
  let count = 0;
  return function () {
    count += 1;
    return count;
  };
}
const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

## Event Delegation

**What is event delegation?**

Event delegation is a technique for handling events in a parent element rather than individual child elements. This is achieved by using event bubbling to catch events at a higher level.

- **Benefits:** Reduces the number of event listeners attached, improves performance, and simplifies event management.
- **Example:**
  ```javascript
  document.getElementById("parent").addEventListener("click", function (event) {
    if (event.target && event.target.matches("button")) {
      console.log("Button clicked!");
    }
  });
  ```

## Event Loop

**What is the event loop?**

The event loop is a mechanism in JavaScript that allows the execution of code, collection of events, and processing of messages. It handles asynchronous operations by managing the call stack and message queue.

- **Call Stack:** Holds the currently executing function.
- **Message Queue:** Holds messages (e.g., events, callbacks) that are waiting to be processed.
- **Process:** When the call stack is empty, the event loop processes messages from the message queue.

## Stack and Queue

**What are stack and queue in JavaScript?**

- **Stack:** A data structure that follows the Last In, First Out (LIFO) principle. JavaScript uses the call stack to manage function execution. Functions are pushed onto the stack and popped off as they complete.

  ```javascript
  function first() {
    second();
  }
  function second() {
    console.log("Second function");
  }
  first(); // Outputs 'Second function'
  ```

- **Queue:** A data structure that follows the First In, First Out (FIFO) principle. JavaScript uses the message queue to manage asynchronous tasks. Messages are processed in the order they are received.
  ```javascript
  setTimeout(() => {
    console.log("Asynchronous task");
  }, 0);
  console.log("Synchronous task");
  // Outputs 'Synchronous task' then 'Asynchronous task'
  ```

## Lexical Context

**What is lexical context in JavaScript?**

Lexical context refers to the environment in which a variable or function is defined. It includes the scope chain and determines variable accessibility. Lexical scoping ensures that functions have access to variables from their defining scope.

Example:

```javascript
function outer() {
  let outerVar = "I am from outer";
  function inner() {
    console.log(outerVar); // Accesses variable from outer function
  }
  inner();
}
outer(); // Outputs 'I am from outer'
```

## First-Class Functions

**What are first-class functions?**

In JavaScript, functions are first-class citizens, meaning they can be:

- **Assigned to Variables:** Functions can be stored in variables.

  ```javascript
  const greet = function () {
    console.log("Hello!");
  };
  greet();
  ```

- **Passed as Arguments:** Functions can be passed as arguments to other functions.

  ```javascript
  function execute(fn) {
    fn();
  }
  execute(() => console.log("Executed!"));
  ```

- **Returned from Functions:** Functions can be returned from other functions.
  ```javascript
  function createMultiplier(multiplier) {
    return function (value) {
      return value * multiplier;
    };
  }
  const double = createMultiplier(2);
  console.log(double(5)); // 10
  ```

## Execution Context

**What is the execution context in JavaScript?**

The execution context is an abstract environment in which JavaScript code is executed. It includes:

- **Global Context:** The default context where code runs outside of any function.
- **Function Context:** Created when a function is invoked, including its own variables, scope chain, and `this` binding.
- **Eval Context:** Created when `eval()` is executed, which is generally avoided due to security concerns.

Each context has its own scope chain and `this` binding.

## JavaScript Asynchronous Working

**How does asynchronous working function in JavaScript?**

JavaScript handles asynchronous operations using:

- **Callbacks:** Functions passed as arguments to other functions, which are executed once a task completes.

  ```javascript
  setTimeout(() => {
    console.log("Callback executed");
  }, 1000);
  ```

- **Promises:** Objects that represent the eventual completion (or failure) of an asynchronous operation.

  ```javascript
  new Promise((resolve, reject) => {
    setTimeout(() => resolve("Promise resolved"), 1000);
  }).then(console.log);
  ```

- **Async/Await:** Syntactic sugar over promises, allowing asynchronous code to be written in a synchronous-like manner.
  ```javascript
  async function fetchData() {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  }
  fetchData();
  ```

## **How can you copy an object by value, not by reference, in JavaScript?**

To copy an object by value in JavaScript, you can use methods like:

- **Shallow Copy:**
  - `Object.assign({}, originalObject)`
  - `{...originalObject}`
- **Deep Copy:**
  - `JSON.parse(JSON.stringify(originalObject))`
  - Libraries like Lodash with `_.cloneDeep(originalObject)`

Shallow copies only copy the top-level properties, while deep copies clone the entire object, including nested properties.

## **What is the `this` keyword in an arrow function in JavaScript?**

In arrow functions, the `this` keyword does not refer to the function itself as it does in regular functions. Instead, it inherits `this` from the surrounding lexical scope, maintaining the context from where the arrow function is defined. This means that `this` in an arrow function is consistent with the `this` of the outer function or context.

```

```

Sure! Here's the question and answer in Markdown format:

````markdown
### Question

Given the following JavaScript code:

```javascript
function b() {
  setTimeout(() => console.log("inside b"), 2000);
}

function a() {
  console.log("inside a");

  b();
  console.log("ended");
}

a();
```
````

How can you modify the code to print the output in the order:

```
inside a
inside b
ended
```

without changing the function definitions of `a` or `b`?

### Answer

To achieve the desired output order without changing the function definitions of `a` or `b`, you can use Promises to control the execution flow. Here's how you can modify the code:

```javascript
function b() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("inside b");
      resolve();
    }, 2000);
  });
}

async function a() {
  console.log("inside a");

  await b();
  console.log("ended");
}

a();
```

#### Explanation:

1. **Promise in `b()`**: The `b()` function is modified to return a `Promise`. When `setTimeout` completes, it logs "inside b" and then calls `resolve()` to indicate that the `Promise` is resolved.

2. **`async` in `a()`**: The `a()` function is modified to be `async`, allowing the use of `await` to pause the execution until `b()` is completed.

3. **`await b()`**: This ensures that `console.log("ended")` is executed only after the `b()` function's `Promise` is resolved, guaranteeing the desired order of outputs.

#### Output:

The modified code will print:

```
inside a
inside b
ended
```

This approach maintains the original structure of `function a` and `function b` but uses Promises to manage asynchronous behavior effectively.

```

```

Here are some similar JavaScript interview questions related to asynchronous behavior, Promises, `async/await`, and execution order:

### 1. **Order of Execution with `setTimeout` and Promises**

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout 1");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise 1");
});

setTimeout(() => {
  console.log("Timeout 2");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise 2");
});

console.log("End");
```

**Question:** What is the order of the console logs? Explain why.

#### **Answer:**

The output will be:

```
Start
End
Promise 1
Promise 2
Timeout 1
Timeout 2
```

**Explanation:**

- JavaScript is single-threaded and uses an event loop to handle asynchronous operations.
- **"Start"** is logged first.
- The `setTimeout` callbacks are added to the macrotask queue and will be executed later.
- Promises are part of the microtask queue, which has a higher priority than the macrotask queue. So, **"Promise 1"** and **"Promise 2"** will be logged before the `setTimeout` callbacks.
- Finally, **"Timeout 1"** and **"Timeout 2"** will be executed in order once the call stack is empty.

---

### 2. **Using `async/await` with Error Handling**

```javascript
async function fetchData() {
  throw new Error("Network Error");
}

async function getData() {
  try {
    await fetchData();
    console.log("Data fetched successfully");
  } catch (error) {
    console.log("Error occurred:", error.message);
  }
}

getData();
```

**Question:** What will be printed to the console? Why?

#### **Answer:**

The output will be:

```
Error occurred: Network Error
```

**Explanation:**

- The `fetchData` function throws an error when called.
- When `await fetchData()` is executed, the `Error` is thrown, and the control is immediately transferred to the `catch` block.
- The `catch` block catches the error and logs **"Error occurred: Network Error"** to the console.

---

### 3. **Chaining Promises and Execution Order**

```javascript
function asyncTask(message, delay) {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log(message);
      resolve();
    }, delay);
  });
}

asyncTask("Task 1", 1000)
  .then(() => asyncTask("Task 2", 500))
  .then(() => asyncTask("Task 3", 300))
  .then(() => console.log("All tasks completed"));
```

**Question:** What will be the order of console logs, and how long will it take to complete all tasks?

#### **Answer:**

The order of the console logs will be:

```
Task 1
Task 2
Task 3
All tasks completed
```

**Explanation:**

- **"Task 1"** is logged after 1 second (1000 milliseconds).
- The next `then` block waits for **"Task 2"** to finish after 500 milliseconds.
- After that, **"Task 3"** will be logged after 300 milliseconds.
- Finally, **"All tasks completed"** is logged.
- The total time taken will be 1000ms + 500ms + 300ms = **1800 milliseconds**.

---

### 4. **Understanding `Promise` Constructor and `then` Method**

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

### 5. **Combining `async/await` with Multiple Promises**

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

### 6. **Mixing `setTimeout` and `Promise` Chaining**

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
