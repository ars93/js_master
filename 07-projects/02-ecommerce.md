# Project 2: E-commerce Platform

## Features
- Product catalog with search & filters
- Shopping cart
- Secure checkout
- Order management
- Admin dashboard
- Payment integration

## Tech Stack
- Frontend: React + Redux
- Backend: Node.js + Express
- Database: MongoDB
- Payment: Stripe

## Database Schema
```
Users
  ├── email
  ├── password
  ├── address
  └── orders

Products
  ├── name
  ├── description
  ├── price
  ├── stock
  ├── images
  └── category

Orders
  ├── user
  ├── items
  ├── total
  ├── status
  └── createdAt
```

## Key Features to Implement

1. **Product Management**
   - List products with pagination
   - Filter by category, price
   - Search functionality

2. **Cart System**
   - Add/remove items
   - Update quantities
   - Persist cart state

3. **Checkout**
   - Collect shipping address
   - Payment processing
   - Order creation

4. **Admin Dashboard**
   - Add/edit products
   - View orders
   - Manage inventory

## Learning Outcomes
- State management with Redux
- Payment gateway integration
- Complex database relationships
- Admin functionality
- Security best practices

---

**Next:** [03-social-media.md](./03-social-media.md)