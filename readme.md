### Frequently Asked JavaScript Interview Questions

### [React Interview Questions](#ReactJS.md)

#### 1. Implement Debounce

**Question:**
Implement a debounce function that delays the processing of the input function until after a specified wait time has elapsed since the last time the debounce function was invoked.

**Code:**
```javascript
function debounce(func, wait) {
  let timeout;
  return function(...args) {
    const context = this;
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(context, args), wait);
  };
}

// Usage
const debouncedFunction = debounce(() => console.log('Debounced!'), 300);
window.addEventListener('resize', debouncedFunction);
```

#### 2. Implement Throttle

**Question:**
Implement a throttle function that ensures a function is called at most once in a specified time interval.

**Code:**
```javascript
function throttle(func, limit) {
  let lastFunc;
  let lastRan;
  return function(...args) {
    const context = this;
    if (!lastRan) {
      func.apply(context, args);
      lastRan = Date.now();
    } else {
      clearTimeout(lastFunc);
      lastFunc = setTimeout(function() {
        if ((Date.now() - lastRan) >= limit) {
          func.apply(context, args);
          lastRan = Date.now();
        }
      }, limit - (Date.now() - lastRan));
    }
  };
}

// Usage
const throttledFunction = throttle(() => console.log('Throttled!'), 1000);
window.addEventListener('resize', throttledFunction);
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
      return function(...args2) {
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
  return arr.reduce((acc, val) => Array.isArray(val) ? acc.concat(deepFlatten(val)) : acc.concat(val), []);
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
  return function(input) {
    return functions.reduce((acc, fn) => fn(acc), input);
  };
}

// Usage
const add = x => x + 1;
const multiply = x => x * 2;
const addThenMultiply = pipe(add, multiply);

console.log(addThenMultiply(5)); // 12
```

#### 6. Implement Auto-retry Promises

**Question:**
Implement a function that retries a promise-returning function a specified number of times before rejecting.

**Code:**
```javascript
function autoRetry(promiseFn, retries) {
  return function(...args) {
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
const unreliableFetch = () => new Promise((resolve, reject) => Math.random() > 0.5 ? resolve('Success') : reject('Failed'));

const fetchWithRetry = autoRetry(unreliableFetch, 3);
fetchWithRetry().then(console.log).catch(console.error);
```

Sure, here's a detailed answer to each of the topics in Markdown format:

---

## Defer & Async Attributes of Script Tag

### Defer
The `defer` attribute tells the browser to download the script in the background while the HTML document is still being parsed. The script is executed after the document has been completely parsed.

```html
<script src="script.js" defer></script>
```

### Async
The `async` attribute also downloads the script in the background, but the script is executed as soon as it is downloaded, without waiting for the HTML parsing to complete.

```html
<script src="script.js" async></script>
```

## Async / Await, Event Loops, Callback Functions

### Async / Await
`async` and `await` are syntactic sugar over promises, providing a cleaner and more intuitive way to work with asynchronous code.

```javascript
async function fetchData() {
    let response = await fetch('https://api.example.com/data');
    let data = await response.json();
    console.log(data);
}
```

### Event Loops
The event loop is a mechanism that allows JavaScript to perform non-blocking operations by offloading operations to the system kernel whenever possible.

### Callback Functions
A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

```javascript
function fetchData(callback) {
    setTimeout(() => {
        callback('Data received');
    }, 1000);
}

fetchData((message) => {
    console.log(message);
});
```

## Promises
A promise is an object representing the eventual completion or failure of an asynchronous operation.

```javascript
let promise = new Promise((resolve, reject) => {
    let success = true;
    if (success) {
        resolve('Operation succeeded');
    } else {
        reject('Operation failed');
    }
});

promise.then((message) => {
    console.log(message);
}).catch((error) => {
    console.error(error);
});
```

## Array Methods

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

## Splice & Slice Difference

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

## Prototype
Prototypes are the mechanism by which JavaScript objects inherit features from one another.

```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
};

let john = new Person('John');
john.greet(); // Hello, my name is John
```

## Difference Between call, bind, apply

### call
Calls a function with a given `this` value and arguments provided individually.

```javascript
function greet(greeting) {
    console.log(`${greeting}, my name is ${this.name}`);
}

let person = { name: 'John' };
greet.call(person, 'Hello'); // Hello, my name is John
```

### apply
Calls a function with a given `this` value and arguments provided as an array.

```javascript
greet.apply(person, ['Hi']); // Hi, my name is John
```

### bind
Creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments.

```javascript
let greetJohn = greet.bind(person, 'Hey');
greetJohn(); // Hey, my name is John
```

## Object Methods

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

## Convert Array to Strings
Convert an array to a string using `toString()`, `join()`, or `JSON.stringify()`.

```javascript
let array = [1, 2, 3, 4, 5];

let str1 = array.toString();
console.log(str1); // "1,2,3,4,5"

let str2 = array.join('-');
console.log(str2); // "1-2-3-4-5"

let str3 = JSON.stringify(array);
console.log(str3); // "[1,2,3,4,5]"
```

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
export const name = 'John';
export function greet() {
    console.log('Hello');
}
```

### Importing

```javascript
// main.js
import { name, greet } from './module.js';
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
localStorage.setItem('name', 'John');
console.log(localStorage.getItem('name')); // John
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
sessionStorage.setItem('name', 'John');
console.log(sessionStorage.getItem('name')); // John
```

### Intersection Observer
Provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.

```javascript
let observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            console.log('Element is in view');
        }
    });
});

observer.observe(document.querySelector('#target'));
```

### WebSocket
Provides a way to open a persistent connection between the client and the server and communicate with messages.

```javascript
let socket = new WebSocket('ws://example.com/socket');

socket.onopen = () => {
    console.log('Connection opened');
    socket.send('Hello Server');
};

socket.onmessage = (event) => {
    console.log('Message from server ', event.data);
};
```

