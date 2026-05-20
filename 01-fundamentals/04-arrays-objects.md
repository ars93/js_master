# 1.4 Arrays & Objects

## Arrays

Ordered collections of values.

### Creating Arrays

```javascript
// Array literal
const fruits = ["apple", "banana", "orange"];

// Array constructor
const numbers = new Array(1, 2, 3, 4, 5);

// Mixed types
const mixed = [1, "hello", true, null, { name: "John" }];

// Nested arrays
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];
```

### Accessing Elements

```javascript
const colors = ["red", "green", "blue"];

console.log(colors[0]);      // "red"
console.log(colors[2]);      // "blue"
console.log(colors.length);  // 3
console.log(colors[-1]);     // undefined (no negative indexing)
```

### Adding & Removing Elements

```javascript
const items = ["a", "b", "c"];

// Add to end
items.push("d");           // ["a", "b", "c", "d"]
const last = items.pop();  // "d", array: ["a", "b", "c"]

// Add to start
items.unshift("z");        // ["z", "a", "b", "c"]
const first = items.shift(); // "z", array: ["a", "b", "c"]

// At specific index
items.splice(1, 0, "x");   // Insert at index 1
items.splice(1, 1);        // Remove 1 element at index 1
```

### Array Methods

#### indexOf & includes

```javascript
const numbers = [1, 2, 3, 4, 5];

console.log(numbers.indexOf(3));    // 2
console.log(numbers.indexOf(10));   // -1 (not found)
console.log(numbers.includes(4));   // true
console.log(numbers.includes(10));  // false
```

#### slice (doesn't modify original)

```javascript
const items = ["a", "b", "c", "d", "e"];

console.log(items.slice(1, 3));  // ["b", "c"]
console.log(items.slice(2));     // ["c", "d", "e"]
console.log(items.slice(-2));    // ["d", "e"]
```

#### join & split

```javascript
const words = ["hello", "world", "from", "JS"];
const sentence = words.join(" ");
console.log(sentence); // "hello world from JS"

const text = "apple,banana,orange";
const fruits = text.split(",");
console.log(fruits); // ["apple", "banana", "orange"]
```

#### map - Transform each element

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

const users = [
  { id: 1, name: "John" },
  { id: 2, name: "Jane" }
];
const names = users.map(user => user.name);
console.log(names); // ["John", "Jane"]
```

#### filter - Keep matching elements

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // [2, 4, 6, 8, 10]

const users = [
  { name: "John", age: 25 },
  { name: "Jane", age: 30 },
  { name: "Bob", age: 17 }
];

const adults = users.filter(user => user.age >= 18);
// [{name: "John", age: 25}, {name: "Jane", age: 30}]
```

#### reduce - Combine into single value

```javascript
const numbers = [1, 2, 3, 4, 5];

// Sum
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 15

// Product
const product = numbers.reduce((acc, num) => acc * num, 1);
console.log(product); // 120

// Count occurrences
const words = ["apple", "banana", "apple", "cherry", "apple"];
const count = words.reduce((acc, word) => {
  acc[word] = (acc[word] || 0) + 1;
  return acc;
}, {});
console.log(count); // {apple: 3, banana: 1, cherry: 1}
```

#### find & findIndex

```javascript
const users = [
  { id: 1, name: "John" },
  { id: 2, name: "Jane" },
  { id: 3, name: "Bob" }
];

const user = users.find(u => u.id === 2);
console.log(user); // {id: 2, name: "Jane"}

const index = users.findIndex(u => u.name === "Bob");
console.log(index); // 2
```

#### some & every

```javascript
const numbers = [1, 2, 3, 4, 5];

// At least one matches
const hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true

// All match
const allPositive = numbers.every(num => num > 0);
console.log(allPositive); // true
```

---

## Objects

Key-value collections.

### Creating Objects

```javascript
// Object literal
const user = {
  name: "John",
  age: 30,
  email: "john@example.com"
};

// Constructor
const car = new Object();
car.brand = "Toyota";
car.model = "Camry";
```

### Accessing Properties

```javascript
const user = { name: "John", age: 30 };

// Dot notation
console.log(user.name);    // "John"

// Bracket notation
console.log(user["age"]);  // 30
console.log(user["name"]); // "John"

// Useful when key is dynamic
const key = "age";
console.log(user[key]);    // 30
```

### Modifying Properties

```javascript
const user = { name: "John", age: 30 };

user.age = 31;           // Modify
user.city = "NYC";       // Add
delete user.age;         // Delete

console.log(user); // {name: "John", city: "NYC"}
```

### Methods in Objects

```javascript
const user = {
  name: "John",
  age: 30,
  greet() {
    console.log(`Hello, I'm ${this.name}`);
  },
  haveBirthday() {
    this.age++;
  }
};

user.greet();       // "Hello, I'm John"
user.haveBirthday();
console.log(user.age); // 31
```

### Destructuring Objects

```javascript
const user = { name: "John", age: 30, city: "NYC" };

// Extract properties
const { name, age } = user;
console.log(name); // "John"
console.log(age);  // 30

// Rename variables
const { name: userName, age: userAge } = user;
console.log(userName); // "John"

// Default values
const { name, country = "USA" } = user;
console.log(country); // "USA"

// Rest operator
const { name, ...rest } = user;
console.log(rest); // {age: 30, city: "NYC"}
```

### Spread Operator with Objects

```javascript
const user = { name: "John", age: 30 };
const job = { title: "Developer", salary: 80000 };

// Merge
const person = { ...user, ...job };
console.log(person);
// {name: "John", age: 30, title: "Developer", salary: 80000}

// Copy and modify
const updated = { ...user, age: 31, city: "NYC" };
console.log(updated);
// {name: "John", age: 31, city: "NYC"}
```

### Object Methods

```javascript
const user = { name: "John", age: 30, email: "john@example.com" };

// Keys
const keys = Object.keys(user);
console.log(keys); // ["name", "age", "email"]

// Values
const values = Object.values(user);
console.log(values); // ["John", 30, "john@example.com"]

// Entries
const entries = Object.entries(user);
console.log(entries);
// [["name", "John"], ["age", 30], ["email", "john@example.com"]]

// Check if property exists
console.log("name" in user);      // true
console.log(user.hasOwnProperty("age")); // true

// Assign (copy properties)
const target = {};
Object.assign(target, user);
console.log(target); // {name: "John", age: 30, email: "john@example.com"}
```

---

## Practical Examples

### Example 1: Student Grading System

```javascript
const students = [
  { name: "Alice", score: 85 },
  { name: "Bob", score: 92 },
  { name: "Charlie", score: 78 },
  { name: "Diana", score: 88 }
];

// Get names of students with score >= 80
const topStudents = students
  .filter(s => s.score >= 80)
  .map(s => s.name);

console.log(topStudents); // ["Alice", "Bob", "Diana"]

// Average score
const avgScore = students.reduce((sum, s) => sum + s.score, 0) / students.length;
console.log(avgScore); // 85.75
```

### Example 2: Shopping Cart

```javascript
const cart = [
  { item: "Apple", price: 1.5, quantity: 3 },
  { item: "Banana", price: 0.75, quantity: 2 },
  { item: "Orange", price: 2, quantity: 4 }
];

// Total price
const total = cart.reduce((sum, product) => {
  return sum + (product.price * product.quantity);
}, 0);

console.log(`Total: $${total.toFixed(2)}`); // Total: $16.50

// Items list
const items = cart.map(p => `${p.item} x${p.quantity}`);
console.log(items);
// ["Apple x3", "Banana x2", "Orange x4"]
```

---

## ✅ Practice Exercises

### Exercise 1: Array Methods
```javascript
// Given: [1, 2, 3, 4, 5]
// Use map to create squares: [1, 4, 9, 16, 25]
// Use filter to get even numbers: [2, 4]
// Use reduce to get sum: 15
```

### Exercise 2: Object Operations
```javascript
// Create a user object with name, age, email
// Use destructuring to extract values
// Merge with another object using spread operator
```

---

## 🎯 Key Takeaways

✅ Arrays are ordered, use numeric indexes  
✅ map, filter, reduce are powerful transformations  
✅ Objects store key-value pairs  
✅ Destructuring simplifies code  
✅ Spread operator for copying and merging  

---

**Next:** [05-dom-manipulation.md](./05-dom-manipulation.md)