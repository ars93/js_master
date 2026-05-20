# 1.3 Functions & Scope

Functions are reusable blocks of code. Scope determines where variables are accessible.

## Function Basics

### Function Declaration

```javascript
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet("John")); // "Hello, John!"
```

### Function Parameters & Arguments

```javascript
// Parameters defined in function
function add(a, b) {
  return a + b;
}

// Arguments passed when calling
console.log(add(5, 3)); // 8

// Default parameters
function welcome(name = "Guest") {
  return `Welcome, ${name}!`;
}

console.log(welcome());        // "Welcome, Guest!"
console.log(welcome("Alice")); // "Welcome, Alice!"
```

### Return Statement

```javascript
function isEven(num) {
  if (num % 2 === 0) {
    return true;
  }
  return false;
  // Code after return never runs
}

console.log(isEven(4));  // true
console.log(isEven(7));  // false
```

---

## Arrow Functions

Modern syntax for functions.

### Basic Arrow Function

```javascript
const add = (a, b) => {
  return a + b;
};

console.log(add(5, 3)); // 8
```

### Concise Arrow Function

If only one line, can omit braces and return:

```javascript
const square = (x) => x * x;
console.log(square(5)); // 25

const cube = x => x * x * x; // Single parameter, no parentheses
console.log(cube(3)); // 27

const getName = () => "John"; // No parameters
console.log(getName()); // "John"
```

### Arrow Functions vs Regular Functions

Key difference: `this` binding

```javascript
const user = {
  name: "John",
  greetRegular: function() {
    console.log(`Hello, I'm ${this.name}`); // 'this' works
  },
  greetArrow: () => {
    console.log(`Hello, I'm ${this.name}`); // 'this' doesn't work
  }
};

user.greetRegular(); // "Hello, I'm John"
user.greetArrow();   // "Hello, I'm undefined"
```

---

## Scope

Scope determines where variables are accessible.

### Global Scope

```javascript
const globalVar = "I'm global";

function test() {
  console.log(globalVar); // Can access global
}

test(); // "I'm global"
console.log(globalVar); // "I'm global"
```

### Function Scope

```javascript
function test() {
  const localVar = "I'm local";
  console.log(localVar); // "I'm local"
}

test();
console.log(localVar); // ReferenceError - not accessible outside
```

### Block Scope (let & const)

```javascript
if (true) {
  let blockVar = "I'm block scoped";
  const blockConst = "Also block scoped";
}

console.log(blockVar);   // ReferenceError
console.log(blockConst); // ReferenceError

// var is NOT block-scoped
if (true) {
  var functionVar = "Function scoped";
}
console.log(functionVar); // "Function scoped" - accessible!
```

### Scope Chain

Inner functions can access outer scope.

```javascript
const outer = "Outer";

function outerFunc() {
  const middle = "Middle";
  
  function innerFunc() {
    const inner = "Inner";
    console.log(inner);   // "Inner"
    console.log(middle);  // "Middle"
    console.log(outer);   // "Outer"
  }
  
  innerFunc();
}

outerFunc();
```

---

## Closures

A function that remembers variables from its outer scope.

### Basic Closure

```javascript
function outer() {
  const message = "I'm captured";
  
  function inner() {
    console.log(message); // Has access to outer's variables
  }
  
  return inner;
}

const closure = outer();
closure(); // "I'm captured"
```

### Practical: Counter

```javascript
function createCounter() {
  let count = 0;
  
  return {
    increment() {
      return ++count;
    },
    decrement() {
      return --count;
    },
    getCount() {
      return count;
    }
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.decrement()); // 1
console.log(counter.getCount());  // 1
```

### Practical: Private Variables

```javascript
function createBankAccount(initialBalance) {
  let balance = initialBalance; // Private
  
  return {
    deposit(amount) {
      balance += amount;
      return balance;
    },
    withdraw(amount) {
      if (amount > balance) {
        return "Insufficient funds";
      }
      balance -= amount;
      return balance;
    },
    getBalance() {
      return balance;
    }
  };
}

const account = createBankAccount(1000);
console.log(account.deposit(500));   // 1500
console.log(account.withdraw(200));  // 1300
console.log(account.balance);        // undefined - private!
console.log(account.getBalance());   // 1300
```

---

## Higher-Order Functions

Functions that take or return other functions.

### Function as Parameter

```javascript
function greet(name, callback) {
  const greeting = `Hello, ${name}!`;
  callback(greeting);
}

greet("John", (msg) => {
  console.log(msg);
}); // "Hello, John!"
```

### Function as Return Value

```javascript
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

---

## Practical Examples

### Example 1: Calculator

```javascript
const calculator = {
  value: 0,
  
  add(n) {
    this.value += n;
    return this;
  },
  
  subtract(n) {
    this.value -= n;
    return this;
  },
  
  multiply(n) {
    this.value *= n;
    return this;
  },
  
  getResult() {
    return this.value;
  }
};

const result = calculator
  .add(10)
  .subtract(3)
  .multiply(2)
  .getResult();

console.log(result); // (10 - 3) * 2 = 14
```

### Example 2: Memoization

```javascript
function memoize(fn) {
  const cache = {};
  
  return function(n) {
    if (n in cache) {
      console.log("From cache");
      return cache[n];
    }
    const result = fn(n);
    cache[n] = result;
    return result;
  };
}

const fibonacci = memoize((n) => {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
});

console.log(fibonacci(5)); // Calculated
console.log(fibonacci(5)); // From cache
```

---

## ✅ Practice Exercises

### Exercise 1: Simple Function
```javascript
// Create a function that calculates area of a rectangle
```

### Exercise 2: Closure
```javascript
// Create a counter function using closure
```

### Exercise 3: Higher-Order
```javascript
// Create a function that returns a function
```

---

## 🎯 Key Takeaways

✅ Functions are reusable code blocks  
✅ Arrow functions have different `this` binding  
✅ Scope determines variable accessibility  
✅ Closures capture outer scope variables  
✅ Higher-order functions are powerful for composition  

---

**Next:** [04-arrays-objects.md](./04-arrays-objects.md)