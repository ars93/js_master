# Project 1: Todo Application

## Features
- User authentication
- Create, read, update, delete todos
- Mark todos as complete
- Filter by status
- Responsive UI

## Tech Stack
- Frontend: React
- Backend: Node.js + Express
- Database: MongoDB
- Auth: JWT

## Structure
```
todo-app/
├── client/ (React)
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   └── services/
├── server/ (Node.js)
│   ├── models/
│   ├── routes/
│   ├── middleware/
│   └── controllers/
└── README.md
```

## Key Implementation Details

### User Registration & Login
- Hash passwords with bcrypt
- Generate JWT tokens
- Store user in MongoDB

### Todo Management
- CRUD operations with authentication
- Update status (complete/incomplete)
- Delete todos

### Frontend
- React hooks for state management
- Fetch todos from API
- Real-time UI updates

## Learning Outcomes
- Complete authentication flow
- RESTful API design
- Database relationships
- Frontend-backend integration
- Error handling

---

**Next:** [02-ecommerce.md](./02-ecommerce.md)