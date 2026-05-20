# 2.1 Closures & Scope Deep Dive

## Understanding Closures

A closure is a function that has access to variables from its outer (enclosing) scope, even after the outer function has returned.

### Basic Closure

```javascript
function outer() {
  const message = "I'm captured"; // Outer variable
  
  function inner() {
    console.log(message); // Inner can access outer
  }
  
  return inner;
}

const closure = outer();
closure(); // "I'm captured"
```

### How It Works

```javascript
function createGreeter(greeting) {
  // greeting is in outer scope
  return function(name) {
    // Can access greeting even after createGreeter returns
    return `${greeting}, ${name}!`;
  };
}

const sayHello = createGreeter("Hello");
const sayHi = createGreeter("Hi");

console.log(sayHello("John")); // "Hello, John!"
console.log(sayHi("Jane"));    // "Hi, Jane!"
```

---

## Practical Closure Patterns

### 1. Data Privacy

```javascript
function createCounter() {
  let count = 0; // Private variable
  
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
console.log(counter.getCount());  // 2
// count variable is private - no direct access
console.log(counter.count);       // undefined
```

### 2. Bank Account with Validation

```javascript
function createBankAccount(initialBalance) {
  let balance = initialBalance;
  const transactions = [];
  
  return {
    deposit(amount) {
      if (amount <= 0) throw new Error("Invalid amount");
      balance += amount;
      transactions.push({ type: "deposit", amount, date: new Date() });
      return balance;
    },
    withdraw(amount) {
      if (amount <= 0) throw new Error("Invalid amount");
      if (amount > balance) throw new Error("Insufficient funds");
      balance -= amount;
      transactions.push({ type: "withdraw", amount, date: new Date() });
      return balance;
    },
    getBalance() {
      return balance;
    },
    getTransactions() {
      return transactions;
    }
  };
}

const account = createBankAccount(1000);
console.log(account.deposit(500));     // 1500
console.log(account.withdraw(200));    // 1300
console.log(account.getBalance());     // 1300
console.log(account.getTransactions()); // Array of transactions
```

### 3. Function Factory

```javascript
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);
const half = createMultiplier(0.5);

console.log(double(10));  // 20
console.log(triple(10));  // 30
console.log(half(10));    // 5
```

### 4. Function Memoization

```javascript
function memoize(fn) {
  const cache = {};
  
  return function(n) {
    if (n in cache) {
      console.log("From cache");
      return cache[n];
    }
    
    console.log("Computing...");
    const result = fn(n);
    cache[n] = result;
    return result;
  };
}

const expensiveFunction = memoize((n) => {
  let result = 0;
  for (let i = 0; i < n; i++) {
    result += i;
  }
  return result;
});

console.log(expensiveFunction(1000)); // "Computing..." → 499500
console.log(expensiveFunction(1000)); // "From cache" → 499500
```

### 5. Event Handler Closures

```javascript
const buttons = document.querySelectorAll("button");

buttons.forEach((btn, index) => {
  btn.addEventListener("click", function() {
    console.log(`Button ${index} clicked`);
  });
});
// Each event handler has access to its own index
```

---

## Common Closure Mistakes

### ❌ The Loop Problem

```javascript
const functions = [];

for (var i = 0; i < 3; i++) {
  functions.push(function() {
    console.log(i);
  });
}

functions[0](); // 3 (not 0!)
functions[1](); // 3 (not 1!)
functions[2](); // 3 (not 2!)

// Why? var is function-scoped, all closures share same i
```

### ✅ Solutions

```javascript
// Solution 1: Use let (block-scoped)
const functions = [];
for (let i = 0; i < 3; i++) {
  functions.push(() => console.log(i));
}
functions[0](); // 0
functions[1](); // 1
functions[2](); // 2

// Solution 2: IIFE (Immediately Invoked Function Expression)
const functions = [];
for (var i = 0; i < 3; i++) {
  functions.push((function(index) {
    return () => console.log(index);
  })(i));
}
functions[0](); // 0
functions[1](); // 1
functions[2](); // 2
```

---

## Performance Considerations

```javascript
// ⚠️ Closures retain references to outer variables
function createBigArray() {
  const largeArray = new Array(1000000).fill(Math.random());
  
  return function() {
    return largeArray[0]; // Closure keeps entire array in memory!
  };
}

// If you don't need the array, clean it up
function createValue() {
  const value = 42;
  
  return function() {
    return value;
  };
}
```

---

## ✅ Practice Exercises

1. Create a secret function that stores a password
2. Build a shopping cart with private state
3. Create a timer function using closures
4. Implement memoization for Fibonacci

---

## 🎯 Key Takeaways

✅ Closures enable data privacy  
✅ Use let/const in loops to avoid closure issues  
✅ Closures keep outer variables in memory  
✅ Powerful pattern for encapsulation  

---

**Next:** [02-async-await.md](./02-async-await.md)