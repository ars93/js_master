# 2.4 Destructuring & Spread Operator

## Array Destructuring

```javascript
const [first, second, third] = [1, 2, 3];
console.log(first); // 1

// Skip elements
const [head, , , tail] = [1, 2, 3, 4];
console.log(head, tail); // 1, 4

// Rest operator
const [one, ...rest] = [1, 2, 3, 4, 5];
console.log(one);  // 1
console.log(rest); // [2, 3, 4, 5]
```

## Object Destructuring

```javascript
const user = { name: "John", age: 30, email: "john@example.com" };

const { name, age } = user;
console.log(name); // "John"

// Rename
const { name: userName, age: userAge } = user;
console.log(userName); // "John"

// Default values
const { name, country = "USA" } = user;
console.log(country); // "USA"
```

## Spread Operator

```javascript
// Arrays
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Objects
const user = { name: "John", age: 30 };
const updated = { ...user, age: 31, city: "NYC" };
console.log(updated);
// { name: "John", age: 31, city: "NYC" }
```

---

**Next:** [05-regex.md](./05-regex.md)