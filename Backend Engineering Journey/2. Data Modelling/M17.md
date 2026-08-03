# Module 17 — API Mapping

> **Goal:** Learn how to convert your business requirements, queries, and data model into clean, predictable, and scalable REST APIs.

---

# Why This Module Matters

Many beginners design APIs like this:

```http
GET /getAllPosts

POST /createPost

PUT /updatePost

DELETE /deletePost
```

These APIs work.

But they don't follow REST principles and become difficult to maintain as applications grow.

Professional backend engineers don't start with endpoints.

They start with:

```text
Business Requirements
        ↓
User Stories
        ↓
Queries
        ↓
Entities
        ↓
REST APIs
```

Your APIs should naturally represent your business.

---

# Where We Are

```text
Requirements
      ↓
Queries
      ↓
Entities
      ↓
Relationships
      ↓
Schema
      ↓
Validation
      ↓
Security
      ↓
API Mapping   ← You are here
      ↓
Implementation
```

Everything you've learned so far leads to this point.

---

# What Is API Mapping?

API Mapping means:

> **Connecting business operations to HTTP endpoints.**

Example:

Requirement:

```text
Users can create blog posts.
```

API:

```http
POST /posts
```

Requirement:

```text
Users can edit posts.
```

API:

```http
PATCH /posts/:postId
```

Requirement:

```text
Users can delete posts.
```

API:

```http
DELETE /posts/:postId
```

Simple.

Natural.

Predictable.

---

# Step 1 — Start From User Stories

Example:

```text
As a user,

I want to create a post.
```

↓

API:

```http
POST /posts
```

---

```text
As a visitor,

I want to read posts.
```

↓

```http
GET /posts
```

---

```text
As a user,

I want to comment.
```

↓

```http
POST /posts/:postId/comments
```

Notice:

We never invented random endpoint names.

---

# Step 2 — Think in Resources

REST is resource-oriented.

Resources:

```text
Users

Posts

Comments

Categories

Orders

Products
```

Not:

```text
CreatePost

DeletePost

GetPosts
```

Resources become URLs.

---

# HTTP Methods

Use the correct HTTP method.

|Method|Purpose|
|---|---|
|GET|Read|
|POST|Create|
|PUT|Replace entire resource|
|PATCH|Update part of a resource|
|DELETE|Remove resource|

---

# CRUD Mapping

Entity:

```text
Post
```

Operations:

Create

↓

```http
POST /posts
```

Read One

↓

```http
GET /posts/:postId
```

Read Many

↓

```http
GET /posts
```

Update

↓

```http
PATCH /posts/:postId
```

Delete

↓

```http
DELETE /posts/:postId
```

Every entity usually starts with these APIs.

---

# Step 3 — Design Around Resources

Bad:

```http
POST /createUser
```

Good:

```http
POST /users
```

---

Bad:

```http
GET /getProducts
```

Good:

```http
GET /products
```

---

Bad:

```http
DELETE /removeComment
```

Good:

```http
DELETE /comments/:commentId
```

REST APIs are based on **nouns**, not verbs.

---

# Step 4 — Map Relationships

Suppose:

```text
Post

↓

Comment
```

Natural endpoint:

```http
GET /posts/:postId/comments
```

Create:

```http
POST /posts/:postId/comments
```

---

Another:

```text
Course

↓

Lessons
```

Endpoints:

```http
GET /courses/:courseId/lessons
```

```http
POST /courses/:courseId/lessons
```

Relationships naturally become nested resources.

---

# Step 5 — Use Query Parameters

Instead of:

```http
GET /publishedPosts
```

Use:

```http
GET /posts?status=published
```

---

Instead of:

```http
GET /postsByAuthor
```

Use:

```http
GET /posts?author=rahul
```

---

Instead of:

```http
GET /latestPosts
```

Use:

```http
GET /posts?sort=-publishedAt
```

Query parameters make APIs flexible.

---

# Step 6 — Support Pagination

Never return everything.

Bad:

```http
GET /posts
```

↓

Returns:

```text
500,000 posts
```

Better:

```http
GET /posts?page=1&limit=10
```

Or cursor pagination:

```http
GET /posts?cursor=abc123&limit=20
```

Every list endpoint should support pagination.

---

# Step 7 — Support Filtering

Example:

```http
GET /products?
```

Possible filters:

```text
category=laptops

priceMin=500

priceMax=1000

brand=apple
```

One endpoint.

Many combinations.

---

# Step 8 — Support Sorting

Example:

```http
GET /posts?
```

Sort:

```text
sort=-createdAt
```

Newest first.

---

```text
sort=title
```

Alphabetical.

---

Multiple fields:

```text
sort=-likesCount,title
```

Very common.

---

# Step 9 — Support Search

Instead of:

```http
GET /searchPosts
```

Use:

```http
GET /posts?search=node
```

Or:

```http
GET /posts?q=node
```

One endpoint.

Consistent design.

---

# Example — Blog Application

## Posts

Create:

```http
POST /posts
```

---

List:

```http
GET /posts
```

---

Read:

```http
GET /posts/:slug
```

Notice:

We use:

```text
slug
```

instead of:

```text
_id
```

Better URLs.

---

Update:

```http
PATCH /posts/:postId
```

---

Delete:

```http
DELETE /posts/:postId
```

---

# Comments

List:

```http
GET /posts/:postId/comments
```

---

Create:

```http
POST /posts/:postId/comments
```

---

Update:

```http
PATCH /comments/:commentId
```

---

Delete:

```http
DELETE /comments/:commentId
```

---

# Likes

Like:

```http
POST /posts/:postId/likes
```

Unlike:

```http
DELETE /posts/:postId/likes
```

Notice:

No need for:

```http
POST /likePost
```

---

# Followers

Follow:

```http
POST /users/:userId/follow
```

Unfollow:

```http
DELETE /users/:userId/follow
```

---

# Authentication

Register:

```http
POST /auth/register
```

---

Login:

```http
POST /auth/login
```

---

Logout:

```http
POST /auth/logout
```

---

Refresh Token:

```http
POST /auth/refresh-token
```

Authentication endpoints are usually grouped separately.

---

# Example — URL Shortener

Create:

```http
POST /urls
```

---

Redirect:

```http
GET /:shortCode
```

---

Analytics:

```http
GET /urls/:id/analytics
```

---

Delete:

```http
DELETE /urls/:id
```

---

# Example — Todo Application

Tasks:

```http
POST /tasks
```

```http
GET /tasks
```

```http
PATCH /tasks/:taskId
```

```http
DELETE /tasks/:taskId
```

Complete:

```http
PATCH /tasks/:taskId/status
```

Body:

```json
{
  "status": "completed"
}
```

---

# Example — E-commerce

Products:

```http
GET /products
```

```http
POST /products
```

---

Cart:

```http
GET /cart
```

```http
POST /cart/items
```

```http
PATCH /cart/items/:itemId
```

```http
DELETE /cart/items/:itemId
```

---

Orders:

```http
POST /orders
```

```http
GET /orders
```

```http
GET /orders/:orderId
```

---

# Map APIs to Database Queries

Remember Module 2?

Query:

```text
Find latest published posts.
```

API:

```http
GET /posts?status=published
```

Database:

```javascript
find({
    status: "published"
})
.sort({
    publishedAt: -1
})
.limit(10)
```

Everything connects together.

---

# API → Service → Repository

A clean backend flow:

```text
Client
      ↓
API Route
      ↓
Controller
      ↓
Validation Middleware
      ↓
Service
      ↓
Repository
      ↓
Database
```

Example:

```http
POST /posts
```

↓

Controller

↓

Validate

↓

Post Service

↓

Post Repository

↓

MongoDB

This is the architecture used in many production backend systems.

---

# Status Codes

Use proper HTTP status codes.

|Code|Meaning|
|---|---|
|200|Success|
|201|Resource Created|
|204|Success (No Content)|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|
|404|Not Found|
|409|Conflict|
|422|Validation Failed|
|500|Internal Server Error|

Example:

Create Post:

```http
201 Created
```

Delete:

```http
204 No Content
```

Validation Error:

```http
422 Unprocessable Entity
```

---

# Common Beginner Mistakes

## Mistake 1

Using verbs in URLs.

Wrong:

```http
/createPost
```

Correct:

```http
POST /posts
```

---

## Mistake 2

Creating different endpoints for filters.

Wrong:

```http
/latestPosts

/popularPosts

/draftPosts
```

Better:

```http
GET /posts?status=draft

GET /posts?sort=-likesCount
```

---

## Mistake 3

Returning unlimited results.

Always paginate.

---

## Mistake 4

Ignoring HTTP methods.

Don't use:

```http
GET /deletePost
```

Use:

```http
DELETE /posts/:id
```

---

## Mistake 5

Putting business logic in controllers.

Controllers should:

- Receive request
    
- Validate
    
- Call service
    
- Return response
    

Business rules belong in the service layer.

---

# API Design Checklist

Before creating an endpoint, ask:

```text
Which business requirement does this satisfy?

Which resource is involved?

Which HTTP method fits?

Does it need authentication?

Who is authorized?

What validation is required?

Does it need pagination?

Does it need filtering?

Does it need sorting?

Which database query will it execute?
```

---

# Blog API Summary

|Requirement|API|
|---|---|
|Register|`POST /auth/register`|
|Login|`POST /auth/login`|
|Create Post|`POST /posts`|
|View Posts|`GET /posts`|
|Read Post|`GET /posts/:slug`|
|Update Post|`PATCH /posts/:postId`|
|Delete Post|`DELETE /posts/:postId`|
|Create Comment|`POST /posts/:postId/comments`|
|View Comments|`GET /posts/:postId/comments`|
|Like Post|`POST /posts/:postId/likes`|
|Unlike Post|`DELETE /posts/:postId/likes`|
|Follow User|`POST /users/:userId/follow`|
|Unfollow User|`DELETE /users/:userId/follow`|

Notice how every endpoint maps directly to a business action.

---

# Best Practices

- Design APIs from business requirements, not from database tables.
    
- Use nouns for resources and HTTP methods for actions.
    
- Support filtering, sorting, searching, and pagination through query parameters.
    
- Keep controllers thin and move business logic into services.
    
- Use meaningful HTTP status codes.
    
- Ensure every API maps cleanly to your underlying queries and indexes.
    

---

# Module 17 Summary

By the end of this module, you should be able to:

- Convert business requirements into RESTful APIs.
    
- Choose appropriate HTTP methods.
    
- Design resource-oriented URLs.
    
- Map relationships to nested endpoints.
    
- Implement filtering, sorting, searching, and pagination consistently.
    
- Connect APIs to controllers, services, repositories, and database queries.
    
- Build predictable and scalable REST APIs.
    

---

# Mini Exercise

Design the REST API for a **Food Delivery Application**.

Entities:

```text
User

Restaurant

MenuItem

Order

DeliveryPartner

Review
```

Requirements:

```text
Users browse restaurants.
Users search menu items.
Users add items to cart.
Users place orders.
Restaurants update order status.
Delivery partners accept deliveries.
Users write reviews.
Admins manage restaurants.
```

For each requirement:

1. Design the REST endpoint.
    
2. Choose the correct HTTP method.
    
3. Decide whether authentication is required.
    
4. Identify request validation rules.
    
5. Map the endpoint to the expected database query.
    
6. Identify which indexes (from Module 12) would make the endpoint efficient.
    

> **Next Module:** **Module 18 — Design Reviews & Trade-offs**, where you'll learn how experienced backend engineers critique a data model before implementation, evaluate alternative designs, justify trade-offs, and answer the "Why did you design it this way?" questions commonly asked in backend interviews.