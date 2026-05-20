# Interview Questions & Answers

## JavaScript Fundamentals

### Q: What's the difference between var, let, and const?
A: 
- var: Function-scoped, can be redeclared (avoid)
- let: Block-scoped, cannot be redeclared
- const: Block-scoped, cannot be reassigned (preferred)

### Q: What is a closure?
A: A function that has access to variables from its outer scope, even after the outer function returns.

### Q: What's the difference between == and ===?
A: == does type coercion, === is strict (no coercion). Always use ===.

## Async & Promises

### Q: What's the difference between promises and callbacks?
A: Callbacks are functions passed as arguments; promises are objects that represent eventual completion or rejection.

### Q: What is async/await?
A: Modern syntax for handling promises that makes asynchronous code look synchronous.

## React

### Q: What's the difference between props and state?
A: Props are passed from parent (read-only), state is internal (mutable).

### Q: When should you use useEffect?
A: For side effects like fetching data, subscriptions, or DOM updates.

## Node.js & Express

### Q: What is middleware?
A: Functions that process requests before they reach route handlers.

### Q: How do you handle errors in Express?
A: Use try-catch in routes and error handler middleware.

---

**Next:** [02-testing.md](./02-testing.md)