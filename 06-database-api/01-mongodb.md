# 6.1 MongoDB

## Collections & Documents

```javascript
// MongoDB is NoSQL
const user = {
  _id: ObjectId(),
  name: "John",
  email: "john@example.com",
  age: 30
};

// Flexible schema
const post = {
  _id: ObjectId(),
  title: "My Post",
  content: "...",
  tags: ["javascript", "nodejs"],
  author: ObjectId() // Reference to user
};
```

## Queries

```javascript
const MongoClient = require('mongodb').MongoClient;

const client = new MongoClient(uri);
const db = client.db('myapp');
const users = db.collection('users');

// Find
const user = await users.findOne({ email: 'john@example.com' });

// Insert
await users.insertOne({ name: 'John', email: 'john@example.com' });

// Update
await users.updateOne({ _id: ObjectId() }, { $set: { age: 31 } });

// Delete
await users.deleteOne({ _id: ObjectId() });
```

---

**Next:** [02-mongoose.md](./02-mongoose.md)