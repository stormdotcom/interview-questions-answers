# JavaScript Output Question

What will be logged to the console when running the following code?

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

console.log(obj.a()); // "undefined"
console.log(obj.b()); // "undefined"
console.log(obj.c()); // "Ajmal"
console.log(obj.d()); // "return a function"
console.log(obj.e()); // "undefined"
console.log(obj.f()()); // "undefined"
console.log(obj.g()); // "undefined"
console.log(obj.h()()); // "undefined"
console.log(obj.i()()); // "undefined"
```
