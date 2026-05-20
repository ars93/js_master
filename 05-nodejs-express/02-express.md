# 5.2 Express Framework

## Basic Server

```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());

// Routes
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.get('/api/users', (req, res) => {
  res.json([{ id: 1, name: 'John' }]);
});

// Start server
app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

## HTTP Methods

```javascript
// GET
app.get('/users/:id', (req, res) => {
  res.json({ id: req.params.id });
});

// POST
app.post('/users', (req, res) => {
  const { name, email } = req.body;
  res.status(201).json({ name, email });
});

// PUT
app.put('/users/:id', (req, res) => {
  res.json({ id: req.params.id, ...req.body });
});

// DELETE
app.delete('/users/:id', (req, res) => {
  res.json({ message: 'Deleted' });
});
```

---

**Next:** [03-routing.md](./03-routing.md)