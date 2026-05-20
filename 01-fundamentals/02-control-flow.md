# 1.2 Control Flow

Control flow statements allow you to decide which code to execute based on conditions.

## If/Else Statements

### Basic if

```javascript
const age = 18;

if (age >= 18) {
  console.log("You can vote");
}
```

### if/else

```javascript
const score = 75;

if (score >= 80) {
  console.log("Pass");
} else {
  console.log("Fail");
}
```

### if/else if/else

```javascript
const age = 20;

if (age >= 65) {
  console.log("Senior");
} else if (age >= 18) {
  console.log("Adult");
} else if (age >= 13) {
  console.log("Teenager");
} else {
  console.log("Child");
}
```

### Practical Example: Grade Assignment

```javascript
const score = 85;
let grade;

if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else if (score >= 70) {
  grade = "C";
} else if (score >= 60) {
  grade = "D";
} else {
  grade = "F";
}

console.log(`Score: ${score}, Grade: ${grade}`); // "Score: 85, Grade: B"
```

---

## Switch Statements

Use switch when comparing one value against many options.

### Basic Switch

```javascript
const day = 3;
let dayName;

switch (day) {
  case 1:
    dayName = "Monday";
    break;
  case 2:
    dayName = "Tuesday";
    break;
  case 3:
    dayName = "Wednesday";
    break;
  case 4:
    dayName = "Thursday";
    break;
  case 5:
    dayName = "Friday";
    break;
  default:
    dayName = "Weekend";
}

console.log(dayName); // "Wednesday"
```

### Switch with User Input

```javascript
const command = "start";

switch (command) {
  case "start":
    console.log("Starting...");
    break;
  case "stop":
    console.log("Stopping...");
    break;
  case "restart":
    console.log("Restarting...");
    break;
  default:
    console.log("Unknown command");
}
```

⚠️ **Important:** Don't forget `break;` or code will "fall through" to next case!

---

## Ternary Operator

Shorthand for if/else (condition ? true : false)

### Basic Ternary

```javascript
const age = 20;
const status = age >= 18 ? "Adult" : "Minor";
console.log(status); // "Adult"
```

### Nested Ternary

```javascript
const score = 85;
const grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
console.log(grade); // "B"
```

### Practical: Discount Calculator

```javascript
const purchaseAmount = 150;
const isMember = true;

const discountPercent = purchaseAmount >= 100 && isMember ? 20 : purchaseAmount >= 100 ? 10 : 0;
const discount = (purchaseAmount * discountPercent) / 100;
const finalPrice = purchaseAmount - discount;

console.log(`Original: $${purchaseAmount}, Discount: ${discountPercent}%, Final: $${finalPrice.toFixed(2)}`);
// Original: $150, Discount: 20%, Final: $120.00
```

---

## Loops

### for Loop

Run code a specific number of times.

```javascript
// Basic for loop
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}

// Loop through array
const fruits = ["apple", "banana", "orange"];
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}

// Countdown
for (let i = 10; i > 0; i--) {
  console.log(i);
}
console.log("Blast off!");
```

### while Loop

Run code while condition is true.

```javascript
let count = 0;
while (count < 5) {
  console.log(count);
  count++;
}

// Real-world: Process items
const queue = ["task1", "task2", "task3"];
while (queue.length > 0) {
  const task = queue.shift(); // Remove first item
  console.log(`Processing: ${task}`);
}
```

### do...while Loop

Run code at least once, then check condition.

```javascript
let x = 0;
do {
  console.log(x);
  x++;
} while (x < 5);

// Real-world: Game loop
let guess;
do {
  guess = Math.floor(Math.random() * 10);
  console.log(`I guessed: ${guess}`);
} while (guess !== 5); // Keep guessing until correct
```

### for...of Loop

Loop through array values (modern syntax).

```javascript
const numbers = [1, 2, 3, 4, 5];

for (const num of numbers) {
  console.log(num); // 1, 2, 3, 4, 5
}

// With strings
const word = "hello";
for (const letter of word) {
  console.log(letter); // h, e, l, l, o
}
```

### for...in Loop

Loop through object keys.

```javascript
const user = {
  name: "John",
  age: 30,
  city: "NYC"
};

for (const key in user) {
  console.log(`${key}: ${user[key]}`);
}
// name: John
// age: 30
// city: NYC
```

---

## Break and Continue

### break - Exit loop early

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Exit loop
  }
  console.log(i); // 0, 1, 2, 3, 4
}

// Real-world: Find item in list
const items = ["apple", "banana", "cherry", "date"];
for (const item of items) {
  if (item === "cherry") {
    console.log("Found it!");
    break;
  }
}
```

### continue - Skip to next iteration

```javascript
for (let i = 0; i < 5; i++) {
  if (i === 2) {
    continue; // Skip this iteration
  }
  console.log(i); // 0, 1, 3, 4
}

// Real-world: Process valid items only
const numbers = [1, 2, -3, 4, -5, 6];
for (const num of numbers) {
  if (num < 0) {
    continue; // Skip negative numbers
  }
  console.log(num); // 1, 2, 4, 6
}
```

---

## Practical Examples

### Example 1: Multiplication Table

```javascript
const num = 5;
console.log(`Multiplication table of ${num}:`);

for (let i = 1; i <= 10; i++) {
  console.log(`${num} × ${i} = ${num * i}`);
}
```

### Example 2: Check Even/Odd Numbers

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const evens = [];
const odds = [];

for (const num of numbers) {
  if (num % 2 === 0) {
    evens.push(num);
  } else {
    odds.push(num);
  }
}

console.log("Even:", evens); // [2, 4, 6, 8, 10]
console.log("Odd:", odds);   // [1, 3, 5, 7, 9]
```

### Example 3: Find Maximum Value

```javascript
const scores = [45, 89, 23, 92, 67, 78, 95, 34];
let max = scores[0];

for (let i = 1; i < scores.length; i++) {
  if (scores[i] > max) {
    max = scores[i];
  }
}

console.log("Highest score:", max); // 95
```

### Example 4: Password Validator

```javascript
const password = "MyP@ssw0rd";
let isValid = true;
let issues = [];

if (password.length < 8) {
  isValid = false;
  issues.push("Too short");
}
if (!/[A-Z]/.test(password)) {
  isValid = false;
  issues.push("No uppercase");
}
if (!/[0-9]/.test(password)) {
  isValid = false;
  issues.push("No number");
}
if (!/[!@#$%^&*]/.test(password)) {
  isValid = false;
  issues.push("No special character");
}

if (isValid) {
  console.log("Strong password!");
} else {
  console.log("Weak password. Issues:", issues.join(", "));
}
```

---

## ✅ Practice Exercises

### Exercise 1: Traffic Light
```javascript
// Create a switch statement for traffic light colors
// red: "Stop"
// yellow: "Caution"
// green: "Go"
```

### Exercise 2: Number Range Checker
```javascript
// Write code to check if number is between 1-100
// If yes: "Valid"
// If no: "Invalid"
```

### Exercise 3: Factorial Calculator
```javascript
// Calculate factorial of a number (n! = n × (n-1) × ... × 1)
// Example: 5! = 120
```

### Exercise 4: Prime Number Checker
```javascript
// Check if a number is prime
// Hint: Prime numbers are only divisible by 1 and itself
```

### Exercise 5: Sum of Array
```javascript
// Add all numbers in an array using a loop
// Example: [1, 2, 3, 4, 5] = 15
```

---

## 🎯 Key Takeaways

✅ if/else for conditions  
✅ switch for multiple cases  
✅ for loop for fixed iterations  
✅ while loop for conditional iterations  
✅ for...of for array values  
✅ for...in for object keys  
✅ break to exit early  
✅ continue to skip iteration  

---

**Next:** [03-functions-scope.md](./03-functions-scope.md)