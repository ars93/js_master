# 3.5 Modules & Imports

## ES6 Modules

```javascript
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

export default class Calculator {
  multiply(a, b) {
    return a * b;
  }
}

// main.js
import Calculator, { add, subtract } from './math.js';

console.log(add(5, 3));        // 8
console.log(subtract(5, 3));   // 2

const calc = new Calculator();
console.log(calc.multiply(5, 3)); // 15
```

## Named & Default Exports

```javascript
// utils.js
export const helper1 = () => {};
export const helper2 = () => {};
export default function main() {}

// app.js
import main, { helper1, helper2 } from './utils.js';
// or
import * as utils from './utils.js';
```

---

**Next:** Phase 4: React