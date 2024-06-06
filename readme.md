### Frequently Asked JavaScript Interview Questions

Here are detailed answers to some of the most frequently asked JavaScript interview questions:

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

These are concise answers to some of the commonly asked JavaScript interview questions, implementing key functions that are often required during coding interviews.