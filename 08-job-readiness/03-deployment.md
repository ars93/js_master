# Deployment

## Deploy React to Vercel

```bash
# Create React app
npx create-react-app my-app

# Deploy to Vercel
npm install -g vercel
vercel
```

## Deploy Node.js to Heroku

```bash
# Create app
heroku create my-app

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

## Environment Variables

```javascript
// .env
DB_URI=mongodb+srv://...
JWT_SECRET=your-secret-key
API_KEY=your-api-key

// Access in code
process.env.DB_URI
```

---

**Next:** [04-portfolio.md](./04-portfolio.md)