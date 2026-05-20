# 5.1 Node.js Basics

## Module System

```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = { add };

// app.js
const { add } = require('./math');
console.log(add(5, 3)); // 8
```

## Reading Files

```javascript
const fs = require('fs');

// Async
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) console.error(err);
  console.log(data);
});

// Async with promises
const data = await fs.promises.readFile('file.txt', 'utf8');
console.log(data);
```

## Process & Environment

```javascript
// Access environment variables
console.log(process.env.NODE_ENV);
console.log(process.env.PORT);

// Pass variables
// NODE_ENV=production PORT=3000 node app.js
```

---

**Next:** [02-express.md](./02-express.md)