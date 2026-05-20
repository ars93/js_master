# 3.2 Design Patterns

## Singleton Pattern

```javascript
class Database {
  static #instance = null;
  
  private constructor() {}
  
  static getInstance() {
    if (!Database.#instance) {
      Database.#instance = new Database();
    }
    return Database.#instance;
  }
  
  query(sql) {
    console.log(`Executing: ${sql}`);
  }
}

const db1 = Database.getInstance();
const db2 = Database.getInstance();
console.log(db1 === db2); // true
```

## Factory Pattern

```javascript
class Transport {
  constructor(type) {
    this.type = type;
  }
}

function createTransport(type) {
  switch(type) {
    case 'car':
      return { type: 'car', wheels: 4, honk: () => 'beep!' };
    case 'bike':
      return { type: 'bike', wheels: 2, ring: () => 'ring!' };
    default:
      throw new Error('Unknown transport');
  }
}

const car = createTransport('car');
const bike = createTransport('bike');
```

## Observer Pattern

```javascript
class EventEmitter {
  constructor() {
    this.events = {};
  }
  
  on(event, callback) {
    if (!this.events[event]) {
      this.events[event] = [];
    }
    this.events[event].push(callback);
  }
  
  emit(event, data) {
    if (this.events[event]) {
      this.events[event].forEach(callback => callback(data));
    }
  }
}

const emitter = new EventEmitter();
emitter.on('userLoggedIn', (user) => {
  console.log(`Welcome, ${user}!`);
});
emitter.emit('userLoggedIn', 'John');
```

---

**Next:** [03-functional-programming.md](./03-functional-programming.md)