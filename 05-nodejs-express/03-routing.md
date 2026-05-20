# 5.3 Routing & Middleware

## Custom Middleware

```javascript
const express = require('express');
const app = express();

// Logging middleware
app.use((req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();
});

// Authentication middleware
const authenticate = (req, res, next) => {
  const token = req.headers.authorization;
  if (!token) {
    return res.status(401).json({ error: 'No token' });
  }
  next();
};

app.get('/protected', authenticate, (req, res) => {
  res.json({ message: 'Protected data' });
});
```

## Router

```javascript
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.json([{ id: 1, name: 'John' }]);
});

router.post('/', (req, res) => {
  res.status(201).json(req.body);
});

module.exports = router;

// In main app
const userRouter = require('./routes/users');
app.use('/api/users', userRouter);
```

---

**Next:** [04-error-handling.md](./04-error-handling.md)