# Testing & Quality

## Jest Unit Tests

```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = { add };

// math.test.js
const { add } = require('./math');

describe('Math functions', () => {
  test('add should return sum', () => {
    expect(add(2, 3)).toBe(5);
  });
  
  test('add should handle negative numbers', () => {
    expect(add(-2, 3)).toBe(1);
  });
});
```

## React Testing Library

```javascript
import { render, screen } from '@testing-library/react';
import Counter from './Counter';

test('renders counter', () => {
  render(<Counter />);
  expect(screen.getByText('Count: 0')).toBeInTheDocument();
});
```

## Code Quality

```javascript
// ESLint configuration (.eslintrc.js)
module.exports = {
  env: { browser: true, node: true },
  extends: 'eslint:recommended',
  rules: {
    'no-console': 'warn',
    'no-var': 'error'
  }
};
```

---

**Next:** [03-deployment.md](./03-deployment.md)