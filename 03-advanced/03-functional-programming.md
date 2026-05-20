# 3.3 Functional Programming

## Pure Functions

```javascript
// Pure function - no side effects
const add = (a, b) => a + b;
const multiply = (a, b) => a * b;

// Not pure - modifies external state
let counter = 0;
const increment = () => ++counter;
```

## Higher-Order Functions

```javascript
const compose = (...fns) => (value) => {
  return fns.reduceRight((acc, fn) => fn(acc), value);
};

const add5 = (x) => x + 5;
const multiply2 = (x) => x * 2;

const addThenMultiply = compose(multiply2, add5);
console.log(addThenMultiply(3)); // (3 + 5) * 2 = 16
```

## Currying

```javascript
const curry = (fn) => {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn(...args);
    }
    return (...nextArgs) => curried(...args, ...nextArgs);
  };
};

const add = (a, b, c) => a + b + c;
const curriedAdd = curry(add);

console.log(curriedAdd(1)(2)(3));     // 6
console.log(curriedAdd(1, 2)(3));     // 6
```

---

**Next:** [04-generators.md](./04-generators.md)