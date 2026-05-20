# 5.4 Error Handling

## Try-Catch in Routes

```javascript
app.get('/users/:id', async (req, res) => {
  try {
    const user = await User.findById(req.params.id);
    if (!user) {
      return res.status(404).json({ error: 'Not found' });
    }
    res.json(user);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

## Error Handler Middleware

```javascript
app.use((err, req, res, next) => {
  console.error(err);
  res.status(err.status || 500).json({
    error: err.message,
    status: err.status || 500
  });
});
```

---

**Next:** Phase 6: Database & API