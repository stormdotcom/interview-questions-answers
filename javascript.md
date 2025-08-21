# JavaScript Output Questions

## Question 1

Determine the output of the following code:

```javascript
const obj = {
  dev: "Ajmal",
  a: function () {
    return this.dev;
  },
  b() {
    return this.dev;
  },
  c: () => {
    return this.dev;
  },
  d: function () {
    return (() => {
      return this.dev;
    })();
  },
  e: function () {
    return this.b();
  },
  f: function () {
    return this.b;
  },
  g: function () {
    return this.c();
  },
  h: function () {
    return this.c;
  },
  i: function () {
    return () => {
      return this.dev;
    };
  },
};

console.log(obj.a()); // ?
console.log(obj.b()); // ?
console.log(obj.c()); // ?
console.log(obj.d()); // ?
console.log(obj.e()); // ?
console.log(obj.f()()); // ?
console.log(obj.g()); // ?
console.log(obj.h()()); // ?
console.log(obj.i()()); // ?
```

## Question 2

Determine the output of the following code:

```javascript
console.log(1);
const promise = new Promise((resolve) => {
  console.log(2);
  resolve();
  console.log(3);
});

console.log(4);

promise
  .then(() => {
    console.log(5);
  })
  .then(() => {
    console.log(6);
  });

console.log(7);

setTimeout(() => {
  console.log(8);
}, 10);

setTimeout(() => {
  console.log(9);
}, 0);
```
