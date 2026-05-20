# 3.4 Generators & Iterators

## Generator Functions

```javascript
function* counter() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = counter();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }
```

## Using Generators

```javascript
function* fibonacci(n) {
  let a = 0, b = 1;
  for (let i = 0; i < n; i++) {
    yield a;
    [a, b] = [b, a + b];
  }
}

for (const value of fibonacci(5)) {
  console.log(value); // 0, 1, 1, 2, 3
}
```

---

**Next:** [05-modules.md](./05-modules.md)