# 3.1 Classes & Object-Oriented Programming

## ES6 Classes

```javascript
class Animal {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  speak() {
    console.log(`${this.name} makes a sound`);
  }
}

const dog = new Animal("Rex", 3);
dog.speak(); // "Rex makes a sound"
```

## Inheritance

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(`${this.name} makes a sound`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);
    this.breed = breed;
  }
  
  speak() {
    console.log(`${this.name} barks`);
  }
}

const dog = new Dog("Rex", "Labrador");
dog.speak(); // "Rex barks"
```

## Static Methods

```javascript
class Math {
  static add(a, b) {
    return a + b;
  }
  
  static multiply(a, b) {
    return a * b;
  }
}

console.log(Math.add(5, 3));       // 8
console.log(Math.multiply(5, 3));  // 15
```

## Getters & Setters

```javascript
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
  
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
  
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  }
}

const person = new Person("John", "Doe");
console.log(person.fullName); // "John Doe"
person.fullName = "Jane Smith";
console.log(person.firstName); // "Jane"
```

## Private Fields

```javascript
class BankAccount {
  #balance = 0; // Private field
  
  constructor(initialBalance) {
    this.#balance = initialBalance;
  }
  
  deposit(amount) {
    this.#balance += amount;
  }
  
  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount(1000);
account.deposit(500);
console.log(account.getBalance());  // 1500
console.log(account.#balance);      // SyntaxError - private!
```

---

**Next:** [02-design-patterns.md](./02-design-patterns.md)