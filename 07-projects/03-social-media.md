# Project 3: Social Media Clone

## Features
- User profiles
- Follow/unfollow
- Create posts with images
- Like and comment
- Real-time notifications
- Search users
- Responsive design

## Tech Stack
- Frontend: React
- Backend: Node.js + Express
- Database: MongoDB
- Real-time: Socket.io (optional)
- Image Upload: Cloudinary

## Database Schema
```
Users
  ├── username
  ├── email
  ├── bio
  ├── profilePicture
  ├── followers
  └── following

Posts
  ├── author
  ├── content
  ├── image
  ├── likes
  ├── comments
  └── createdAt

Comments
  ├── author
  ├── post
  ├── content
  └── createdAt
```

## Key Features

1. **User System**
   - Registration & login
   - Profile management
   - Follow system

2. **Post Management**
   - Create posts
   - Upload images
   - Edit/delete posts

3. **Engagement**
   - Like posts
   - Comment on posts
   - View likes/comments

4. **Notifications**
   - Like notifications
   - Comment notifications
   - Follow notifications

## Learning Outcomes
- Complex relationships between entities
- Image upload and storage
- Real-time features
- Feed algorithms
- Performance optimization

---

**Next:** Phase 8: Job Readiness