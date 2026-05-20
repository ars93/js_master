# 6.2 Mongoose ODM

## Schema Definition

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, unique: true },
  age: { type: Number, min: 0 },
  createdAt: { type: Date, default: Date.now }
});

const User = mongoose.model('User', userSchema);
```

## CRUD with Mongoose

```javascript
// Create
const user = await User.create({ name: 'John', email: 'john@example.com' });

// Read
const user = await User.findById(id);
const users = await User.find({ age: { $gte: 18 } });

// Update
await User.findByIdAndUpdate(id, { age: 31 });

// Delete
await User.findByIdAndDelete(id);
```

---

**Next:** [03-jwt.md](./03-jwt.md)