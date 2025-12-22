# 1️⃣6️⃣ Post Routes — `routes/posts.js`

### Purpose

Expose post APIs.

### Pseudocode

```
GET /posts → list posts
GET /posts/:id → get post
POST /posts → create post (auth)
PUT /posts/:id → update post (auth)
DELETE /posts/:id → soft delete (auth)
POST /posts/:id/like → like post
GET /analytics/top-authors → analytics
```

🗣

> “Public and protected routes are clearly separated.”