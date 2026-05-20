# 6.4 CRUD Operations

## Complete REST API

```javascript
const express = require('express');
const mongoose = require('mongoose');
const jwt = require('jsonwebtoken');

const app = express();
app.use(express.json());

// Connect to DB
await mongoose.connect(process.env.MONGODB_URI);

// Schema
const postSchema = new mongoose.Schema({
  title: { type: String, required: true },
  content: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
  createdAt: { type: Date, default: Date.now }
});

const Post = mongoose.model('Post', postSchema);

// Middleware
const verifyToken = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).json({ error: 'No token' });
  
  try {
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
};

// CRUD
app.post('/posts', verifyToken, async (req, res) => {
  const post = await Post.create({ ...req.body, author: req.user.userId });
  res.status(201).json(post);
});

app.get('/posts', async (req, res) => {
  const posts = await Post.find().populate('author', 'name email');
  res.json(posts);
});

app.get('/posts/:id', async (req, res) => {
  const post = await Post.findById(req.params.id);
  if (!post) return res.status(404).json({ error: 'Not found' });
  res.json(post);
});

app.put('/posts/:id', verifyToken, async (req, res) => {
  const post = await Post.findByIdAndUpdate(req.params.id, req.body, { new: true });
  res.json(post);
});

app.delete('/posts/:id', verifyToken, async (req, res) => {
  await Post.findByIdAndDelete(req.params.id);
  res.json({ message: 'Deleted' });
});

app.listen(3000);
```

---

**Next:** Phase 7: Real-World Projects