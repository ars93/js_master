# 1.1 Variables, Data Types & Operators

## 📌 Variables

Variables are containers for storing data values.

### var, let, and const

JavaScript has three ways to declare variables, each with different characteristics.

#### `var` - Function Scoped (AVOID - Old syntax)

```javascript
var x = 10;
var x = 20; // Can redeclare - problematic!
console.log(x); // 20

function test() {
  var y = 5;
}
console.log(y); // ReferenceError - not accessible outside function
```

❌ Problems with `var`:
- Can be redeclared (causes bugs)
- Function-scoped (confusing for block scope)
- Hoisting issues

#### `let` - Block Scoped (Use for variables that change)

```javascript
let name = "John";
name = "Jane"; // OK - can reassign
// let name = "Bob"; // ERROR - cannot redeclare in same scope

if (true) {
  let age = 25;
}
console.log(age); // ReferenceError - block-scoped
```

✅ Advantages:
- Block-scoped (more predictable)
- Cannot be redeclared in same scope
- Modern syntax

#### `const` - Block Scoped, Cannot Reassign (PREFERRED)

```javascript
const PI = 3.14159;
// PI = 3.14; // ERROR - cannot reassign

const user = { name: "John" };
user.name = "Jane"; // OK - object contents can change
// user = {}; // ERROR - cannot reassign variable
```

✅ Advantages:
- Prevents accidental reassignment
- Shows intent (this won't change)
- Recommended in modern JavaScript

### Variable Declaration Best Practices

```javascript
// ✅ GOOD - Use const by default
const MAX_USERS = 100;

// ✅ GOOD - Use let when you need to reassign
let count = 0;
count++; // Reassignment is necessary here

// ❌ AVOID - Never use var
var oldVariable = "outdated";
```

---

## 📊 JavaScript Data Types

JavaScript has 7 primitive types and object types.

### Primitive Data Types

#### 1. **Number**

Represents both integers and decimals.

```javascript
const age = 25;           // Integer
const price = 19.99;      // Decimal
const largeNumber = 1e6;  // Scientific notation = 1000000
const infinity = Infinity;
const notNumber = NaN;    // Not-a-Number

// Math with numbers
console.log(10 + 5);      // 15
console.log(10 / 3);      // 3.3333...
console.log(2 ** 3);      // 8 (exponentiation)
console.log(10 % 3);      // 1 (remainder)

// Number methods
const num = 123.456;
console.log(num.toFixed(2));        // "123.46" - round to 2 decimals
console.log(parseInt("42"));        // 42 - convert string to integer
console.log(parseFloat("3.14"));    // 3.14 - convert string to decimal
```

#### 2. **String**

Represents text data.

```javascript
// Different ways to create strings
const name = "John";              // Double quotes
const city = 'New York';          // Single quotes
const message = `Hello, ${name}`; // Template literal

// String methods
const str = "JavaScript";
console.log(str.length);           // 10
console.log(str.toUpperCase());    // "JAVASCRIPT"
console.log(str.toLowerCase());    // "javascript"
console.log(str.substring(0, 4));  // "Java"
console.log(str.includes("Script")); // true
console.log(str.split(""));        // Array of characters
console.log(str.replace("Java", "Type")); // "TypeScript"

// Template literals with expressions
const hours = 9;
const greeting = `Good morning! It's ${hours} AM`;
console.log(greeting);
```

#### 3. **Boolean**

Represents true or false.

```javascript
const isStudent = true;
const isAdult = false;

// Comparisons return booleans
console.log(10 > 5);      // true
console.log(10 === "10"); // false

// Logical operations
console.log(true && false);  // false
console.log(true || false);  // true
console.log(!true);          // false
```

#### 4. **null**

Represents the intentional absence of value.

```javascript
let user = null; // Explicitly empty
console.log(user); // null
```

#### 5. **undefined**

Represents a variable declared but not assigned.

```javascript
let x;
console.log(x); // undefined

function test() {
  // No return statement
}
console.log(test()); // undefined
```

#### 6. **Symbol** (Advanced)

Creates a unique identifier.

```javascript
const id = Symbol("userId");
const id2 = Symbol("userId");
console.log(id === id2); // false - each symbol is unique
```

### Object Data Types

#### 7. **Objects**

Collections of key-value pairs.

```javascript
const user = {
  name: "John",
  age: 30,
  email: "john@example.com"
};

console.log(user.name); // "John"
console.log(user["age"]); // 30
```

#### 8. **Arrays**

Ordered collections of values.

```javascript
const colors = ["red", "green", "blue"];
console.log(colors[0]); // "red"
console.log(colors.length); // 3
```

#### 9. **Functions**

Reusable blocks of code.

```javascript
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet("John")); // "Hello, John!"
```

---

## 🔄 Type Conversion

### Implicit Type Conversion

JavaScript automatically converts types in some situations (can cause bugs!).

```javascript
console.log("5" + 3);        // "53" - string concatenation
console.log("5" - 3);        // 2 - string converted to number
console.log(true + 1);       // 2 - true is 1, false is 0
console.log(null + 5);       // 5 - null is 0
console.log(undefined + 5);  // NaN
```

### Explicit Type Conversion

Convert types intentionally (safer).

```javascript
// To String
const num = 42;
console.log(String(num));      // "42"
console.log(num.toString());   // "42"
console.log(String(true));     // "true"

// To Number
console.log(Number("42"));     // 42
console.log(Number("3.14"));   // 3.14
console.log(Number(true));     // 1
console.log(Number(false));    // 0
console.log(parseInt("42px")); // 42

// To Boolean
console.log(Boolean(1));       // true
console.log(Boolean(0));       // false
console.log(Boolean(""));      // false
console.log(Boolean("hello")); // true
console.log(Boolean(null));    // false
```

---

## 🧮 Operators

### Arithmetic Operators

```javascript
console.log(10 + 5);    // 15 (addition)
console.log(10 - 5);    // 5 (subtraction)
console.log(10 * 5);    // 50 (multiplication)
console.log(10 / 5);    // 2 (division)
console.log(10 % 3);    // 1 (modulo - remainder)
console.log(2 ** 3);    // 8 (exponentiation)

// Increment and Decrement
let count = 5;
console.log(count++);   // 5 (post-increment - returns before incrementing)
console.log(count);     // 6
console.log(++count);   // 7 (pre-increment - returns after incrementing)
```

### Comparison Operators

```javascript
// Loose comparison (not recommended)
console.log(5 == "5");    // true - compares value, ignores type
console.log(0 == false);  // true

// Strict comparison (recommended)
console.log(5 === "5");   // false - compares value AND type
console.log(5 !== "5");   // true

// Other comparisons
console.log(10 > 5);      // true
console.log(10 >= 10);    // true
console.log(5 < 10);      // true
console.log(5 <= 5);      // true
```

### Logical Operators

```javascript
// AND - both must be true
console.log(true && true);   // true
console.log(true && false);  // false

// OR - at least one must be true
console.log(true || false);  // true
console.log(false || false); // false

// NOT - inverts the boolean
console.log(!true);          // false
console.log(!false);         // true

// Practical example
const age = 25;
const hasLicense = true;

if (age >= 18 && hasLicense) {
  console.log("Can drive");
}
```

### Assignment Operators

```javascript
let x = 10;

x += 5;   // x = x + 5 → 15
x -= 3;   // x = x - 3 → 12
x *= 2;   // x = x * 2 → 24
x /= 6;   // x = x / 6 → 4
x %= 3;   // x = x % 3 → 1
x **= 2;  // x = x ** 2 → 1
```

### Ternary Operator (Conditional Operator)

Short way to write if/else.

```javascript
const age = 20;
const status = age >= 18 ? "Adult" : "Minor";
console.log(status); // "Adult"

// More complex
const score = 85;
const grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
console.log(grade); // "B"
```

---

## 🎯 Practical Examples

### Example 1: Calculate BMI

```javascript
const weight = 70;      // kg
const height = 1.75;    // meters
const bmi = weight / (height * height);

console.log(bmi.toFixed(2)); // "22.86"

let category;
if (bmi < 18.5) {
  category = "Underweight";
} else if (bmi < 25) {
  category = "Normal";
} else if (bmi < 30) {
  category = "Overweight";
} else {
  category = "Obese";
}

console.log(`BMI: ${bmi.toFixed(2)}, Category: ${category}`);
```

### Example 2: Temperature Converter

```javascript
const celsius = 25;
const fahrenheit = (celsius * 9/5) + 32;

console.log(`${celsius}°C = ${fahrenheit}°F`);

// Using template literal
const message = `
  Temperature: ${celsius}°C
  In Fahrenheit: ${fahrenheit.toFixed(1)}°F
  Status: ${fahrenheit > 68 ? "Warm" : "Cold"}
`;
console.log(message);
```

### Example 3: Age Calculator

```javascript
const birthYear = 1995;
const currentYear = 2024;
const age = currentYear - birthYear;

const isAdult = age >= 18;
const canVote = age >= 18;
const canRent = age >= 25;

console.log(`
  Age: ${age}
  Can vote: ${canVote}
  Can rent a car: ${canRent}
`);
```

---

## ✅ Practice Exercises

### Exercise 1: Variables and Data Types
```javascript
// 1. Create variables for your name, age, and city
// 2. Create a template literal that prints: "I am [name], [age] years old, from [city]"
// 3. Try changing the variables and run again

// Answer below:
// const name = "Your Name";
// const age = 25;
// const city = "Your City";
// console.log(`I am ${name}, ${age} years old, from ${city}`);
```

### Exercise 2: Operators
```javascript
// 1. Calculate: (10 + 5) * 2
// 2. Check if 10 > 5 AND 3 < 8
// 3. Use ternary to check if 15 is greater than 10, print "Yes" or "No"

// Answer below:
// console.log((10 + 5) * 2);      // 30
// console.log(10 > 5 && 3 < 8);   // true
// console.log(15 > 10 ? "Yes" : "No"); // "Yes"
```

### Exercise 3: Type Conversion
```javascript
// 1. Convert string "42" to number
// 2. Convert number 100 to string
// 3. Convert "false" to boolean (hint: it becomes true!)

// Answer below:
// console.log(Number("42"));      // 42
// console.log(String(100));       // "100"
// console.log(Boolean("false"));  // true - non-empty string is true!
```

### Exercise 4: Real-World Problem
```javascript
// A store offers 20% discount on purchases over $100
// Calculate the final price for a $150 item

const itemPrice = 150;
const discountThreshold = 100;
const discountRate = 0.20;

const discount = itemPrice > discountThreshold ? itemPrice * discountRate : 0;
const finalPrice = itemPrice - discount;

console.log(`Original: $${itemPrice}, Discount: $${discount}, Final: $${finalPrice}`);
```

---

## 🔍 Checking Your Understanding

- [ ] Can you explain the difference between var, let, and const?
- [ ] Do you know all 7 primitive data types?
- [ ] Can you convert between types?
- [ ] Can you use all arithmetic and logical operators?
- [ ] Can you write and use template literals?

---

## 🔗 Next: [Control Flow](./02-control-flow.md)

Continue learning about if/else statements, loops, and switch statements!
