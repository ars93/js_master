# 2.5 Regular Expressions

## Creating Regular Expressions

```javascript
const regex1 = /hello/i;                    // Literal
const regex2 = new RegExp('hello', 'i');   // Constructor

// Test if matches
console.log(regex1.test('Hello World'));  // true
```

## Common Patterns

```javascript
// Email
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
console.log(emailRegex.test('user@example.com')); // true

// Phone number
const phoneRegex = /^[0-9]{3}-[0-9]{3}-[0-9]{4}$/;
console.log(phoneRegex.test('123-456-7890')); // true

// Password (min 8 chars, uppercase, lowercase, number)
const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/;
console.log(passwordRegex.test('Secure123')); // true
```

## String Methods

```javascript
const text = 'The quick brown fox';

// match
const matches = text.match(/[a-z]+/gi);
console.log(matches); // ['The', 'quick', 'brown', 'fox']

// replace
const replaced = text.replace(/quick/, 'slow');
console.log(replaced); // 'The slow brown fox'

// split
const words = text.split(/\s+/);
console.log(words); // ['The', 'quick', 'brown', 'fox']
```

---

**Next:** Phase 3