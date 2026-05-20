# 2.3 Error Handling

Properly handle errors to create robust applications.

## Try/Catch/Finally

```javascript
try {
  const result = JSON.parse('{invalid json}');
  console.log(result);
} catch (error) {
  console.error("Parse error:", error.message);
} finally {
  console.log("Cleanup");
}
```

## Throwing Errors

```javascript
function validateAge(age) {
  if (age < 0) {
    throw new Error("Age cannot be negative");
  }
  if (age < 18) {
    throw new Error("Must be 18 or older");
  }
  return true;
}

try {
  validateAge(-5);
} catch (error) {
  console.log(error.message);
}
```

## Error Types

```javascript
// TypeError
try {
  const obj = null;
  obj.name; // TypeError: Cannot read property 'name' of null
} catch (error) {
  if (error instanceof TypeError) {
    console.log("Type error:", error.message);
  }
}

// SyntaxError
try {
  JSON.parse('{bad}');
} catch (error) {
  if (error instanceof SyntaxError) {
    console.log("Syntax error:", error.message);
  }
}
```

## Async Error Handling

```javascript
async function safeFetch(url) {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error("Fetch failed:", error.message);
    throw error; // Re-throw if needed
  }
}

// Usage
try {
  const data = await safeFetch("/api/data");
  console.log(data);
} catch (error) {
  console.error("Failed to get data");
}
```

---

**Next:** [04-destructuring-spread.md](./04-destructuring-spread.md)