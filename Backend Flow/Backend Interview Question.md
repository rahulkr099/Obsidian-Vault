These are **very common backend interview questions**. If you understand them clearly, you will answer confidently in interviews. Let’s go step-by-step in **simple words with examples**.

---

# 1. When to use **Params** (`req.params`)?

Use **params** when the value is **part of the URL path** and identifies a **specific resource**.

Example URL

```
GET /todos/123
```

Here `123` is the **todo id**.

Express route

```javascript
app.get("/todos/:id", (req, res) => {
   const id = req.params.id;
   res.send(`Todo id is ${id}`);
});
```

Example responses

```
/todos/1
/todos/55
/todos/abc
```

Use params for things like

- user id
    
- product id
    
- todo id
    
- post id
    

Example APIs

```
GET /users/45
GET /products/100
DELETE /todos/8
```

Think like this:

> Params = **Which specific resource?**

---

# 2. When to use **Query** (`req.query`)?

Use **query** when you want to **filter, sort, search, or paginate data**.

Example

```
GET /todos?status=completed
```

Express

```javascript
app.get("/todos", (req, res) => {
   const status = req.query.status;
   res.send(`Filter todos with status ${status}`);
});
```

More examples

```
GET /todos?page=2
GET /todos?limit=10
GET /todos?sort=createdAt
GET /todos?status=pending
GET /products?category=electronics
```

Example combination

```
GET /todos?status=pending&page=2&limit=10
```

Think like this:

> Query = **How to filter the list**

---

# 3. Params vs Query (Interview Shortcut)

|Feature|Params|Query|
|---|---|---|
|Location|URL path|After `?`|
|Purpose|Identify resource|Filter or modify result|
|Example|`/users/12`|`/users?page=2`|
|Express|`req.params`|`req.query`|

Example combined

```
GET /users/12/posts?page=2
```

```
12 → params
page → query
```

---

# 4. How token is sent in **Authorization header**

When a user logs in, the server gives a **JWT token**.

Example response

```json
{
 "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

Client sends this token in every request.

Request example

```
GET /todos
```

Headers

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

In Express

```javascript
const token = req.headers.authorization;
```

Usually we split it

```javascript
const token = req.headers.authorization.split(" ")[1];
```

Because header looks like

```
Bearer TOKEN
```

---

# 5. Why we validate token in **middleware**

Middleware runs **before the controller**.

So it checks if the user is **authenticated**.

Example flow

```
Request → Middleware → Controller → Response
```

Example middleware

```javascript
import jwt from "jsonwebtoken";

export const verifyToken = (req, res, next) => {

  const authHeader = req.headers.authorization;

  if (!authHeader) {
     return res.status(401).json({message: "No token provided"});
  }

  const token = authHeader.split(" ")[1];

  try {
     const decoded = jwt.verify(token, process.env.JWT_SECRET);
     req.user = decoded;
     next();
  } catch (error) {
     return res.status(401).json({message: "Invalid token"});
  }

};
```

Route usage

```javascript
router.get("/todos", verifyToken, getTodos);
```

Why middleware?

Because

- Avoid repeating code
    
- Central authentication logic
    
- Secure routes
    
- Cleaner controllers
    

---

# 6. Good Interview Question

### Why use **Bearer token**?

Bearer means

> Whoever has the token can access the resource.

Example

```
Authorization: Bearer TOKEN
```

It is the **standard format** for sending JWT tokens.

---

# 7. What happens inside **JWT verification**

Steps

1. Client sends token
    
2. Server receives token
    
3. Server checks signature
    
4. Server checks expiration
    
5. If valid → allow request
    

Example

```javascript
jwt.verify(token, SECRET)
```

---

# 8. Another important interview question

### Where should we store JWT token?

Two common ways

**1️⃣ HttpOnly Cookie (Most Secure)**

```
cookie: accessToken=eyJhbGci...
```

Benefits

- Not accessible by JS
    
- Protects from XSS
    

---

**2️⃣ LocalStorage**

```
localStorage.setItem("token", token)
```

But

- Vulnerable to XSS
    

---

# 9. Very common interview question

### Difference between Authentication and Authorization

|Authentication|Authorization|
|---|---|
|Who are you|What can you access|
|Login|Permissions|
|Example|Admin access|

Example

```
Login → Authentication
Access admin route → Authorization
```

---

# 10. Extra Questions Interviewers Ask

Practice answering these.

### API Questions

- What is REST API?
    
- What is idempotent API?
    
- Difference between PUT and PATCH?
    
- What status code should be returned for creation?
    

Answer

```
POST /users → 201 Created
```

---

### Security Questions

- What is JWT?
    
- What is CORS?
    
- What is rate limiting?
    
- What is Helmet middleware?
    

---

### Backend Questions

- Difference between middleware and controller
    
- Difference between authentication and authorization
    
- What is stateless authentication?
    
- What is refresh token?
    

---

# 11. One strong interview question

### Why not store JWT in database?

Because

JWT is **stateless**.

Server only verifies **signature**, no DB lookup needed.

Benefits

- Faster
    
- Scalable
    
- No session storage
    

---

# Final Advice

Since you are already building a **Todo API**, interviewers may ask:

- Design Todo API
    
- Authentication flow
    
- Error handling
    
- Pagination
    
- Security middleware
    

These topics you are already practicing — that is **excellent preparation**.

---

If you want, I can also show you:

**"20 Backend Interview Questions Every MERN Developer Should Know"**

This will help you **crack backend interviews easily.**

Great! Since you are already building **APIs (Todo App, authentication, middleware, JWT)**, these questions will help you prepare for **backend / MERN interviews**. Try to **practice explaining them in your own words**.

---

# 20 Important Backend Interview Questions (with simple answers)

---

# 1. What is REST API?

REST API is a way for **client and server to communicate using HTTP methods**.

Example

```
GET /todos
POST /todos
PUT /todos/1
DELETE /todos/1
```

Each URL represents a **resource**.

Key principles:

- Stateless
    
- Resource-based
    
- Uses HTTP methods
    

---

# 2. What are HTTP Methods?

|Method|Purpose|
|---|---|
|GET|Read data|
|POST|Create data|
|PUT|Update full resource|
|PATCH|Update partial resource|
|DELETE|Remove resource|

Example

```
POST /todos
```

Creates a new todo.

---

# 3. Difference between PUT and PATCH

**PUT**

- Updates the **entire resource**
    

Example

```
PUT /users/1
```

Send complete user object.

---

**PATCH**

- Updates **only specific fields**
    

Example

```
PATCH /users/1
```

```
{
 "name": "Rahul"
}
```

---

# 4. What is middleware in Express?

Middleware is a **function that runs before the controller**.

Flow

```
Request → Middleware → Controller → Response
```

Example

```javascript
app.use((req,res,next)=>{
   console.log("Request received");
   next();
})
```

---

# 5. What is JWT?

JWT (JSON Web Token) is used for **authentication**.

When user logs in:

1. Server generates token
    
2. Client stores token
    
3. Client sends token with requests
    

Example header

```
Authorization: Bearer TOKEN
```

---

# 6. What is Authentication?

Authentication means:

> Verifying the identity of the user.

Example

```
Login with email and password
```

Server checks if user exists.

---

# 7. What is Authorization?

Authorization means:

> Checking what the user is allowed to access.

Example

```
Admin → delete users
Normal user → cannot delete users
```

---

# 8. What is CORS?

CORS means **Cross Origin Resource Sharing**.

It allows frontend and backend from **different domains** to communicate.

Example

```
Frontend: localhost:5173
Backend: localhost:3000
```

We enable CORS:

```javascript
import cors from "cors"
app.use(cors())
```

---

# 9. What is Rate Limiting?

Rate limiting prevents **too many requests from a user**.

Example

```
100 requests per minute
```

Express example

```javascript
import rateLimit from "express-rate-limit"
```

Used to prevent

- brute force attacks
    
- spam requests
    

---

# 10. What is Helmet?

Helmet adds **security headers** to Express apps.

Example

```javascript
import helmet from "helmet"
app.use(helmet())
```

It protects against:

- XSS
    
- clickjacking
    
- content sniffing
    

---

# 11. What is Idempotent API?

An API is **idempotent** if calling it multiple times gives the **same result**.

Example

```
DELETE /todos/1
DELETE /todos/1
```

Result is still

```
Todo deleted
```

Methods that are idempotent:

```
GET
PUT
DELETE
```

---

# 12. What is Pagination?

Pagination means **loading data in small chunks**.

Example

```
GET /todos?page=2&limit=10
```

Benefits

- Faster response
    
- Better performance
    
- Less memory usage
    

---

# 13. What is indexing in MongoDB?

Indexing improves **query performance**.

Example

```javascript
db.users.createIndex({ email: 1 })
```

Now searching by email is faster.

---

# 14. What is MVC architecture?

MVC means:

|Layer|Purpose|
|---|---|
|Model|Database|
|View|UI|
|Controller|Logic|

In backend:

```
routes → controllers → models
```

Example

```
routes/todo.routes.js
controllers/todo.controller.js
models/todo.model.js
```

---

# 15. What is async/await?

Used for **handling asynchronous operations**.

Example

```javascript
const users = await User.find()
```

Instead of

```javascript
User.find().then()
```

---

# 16. What is error handling middleware?

It catches errors globally.

Example

```javascript
app.use((err, req, res, next)=>{
   res.status(500).json({
      message: err.message
   })
})
```

Prevents server crash.

---

# 17. What is environment variable?

Used to store **secret information**.

Example `.env`

```
PORT=3000
JWT_SECRET=abc123
DB_URL=mongodb://localhost
```

Access in code

```javascript
process.env.JWT_SECRET
```

---

# 18. What is hashing?

Hashing protects passwords.

Example

```
bcrypt.hash(password)
```

Stored password looks like

```
$2b$10$gkdlflskdlfjlsdf
```

Not the original password.

---

# 19. Difference between SQL and NoSQL

|SQL|NoSQL|
|---|---|
|Structured tables|Flexible documents|
|MySQL|MongoDB|
|Fixed schema|Dynamic schema|

Example MongoDB

```json
{
 "name": "Rahul",
 "skills": ["node","react"]
}
```

---

# 20. How does a request flow in Express?

Flow

```
Client
   ↓
Route
   ↓
Middleware
   ↓
Controller
   ↓
Database
   ↓
Response
```

Example

```
GET /todos
```

Flow

```
route → authMiddleware → controller → DB → response
```

---

# Bonus Question (Interviewers love this)

### How would you design a Todo API?

Endpoints

```
POST /todos
GET /todos
GET /todos/:id
PATCH /todos/:id
DELETE /todos/:id
```

With authentication

```
POST /login
POST /register
```

---

# Small Tip for Your Interviews

When answering backend questions:

Always mention **3 things**

1️⃣ Security  
2️⃣ Performance  
3️⃣ Scalability

Interviewers love hearing these.

Example answer:

> "We use JWT middleware for authentication, pagination for performance, and indexing for faster queries."

That sounds **very professional**.

---

If you want, I can also show you something extremely useful:

**"10 Backend System Design Questions for Junior Developers"**

These are asked in **MERN / Node.js interviews very frequently.** 🚀

Great! These **System Design questions** are often asked even for **junior backend developers**. Interviewers usually want to see **how you think**, not perfect answers. So learn the **structure of answering**.

I’ll show you **10 common system design questions** and **how to answer them simply**.

---

# 1. Design a Todo API

This is very similar to what you already built.

### Main entities

```
User
Todo
Activity (optional)
```

### Endpoints

```
POST   /auth/register
POST   /auth/login

POST   /todos
GET    /todos
GET    /todos/:id
PATCH  /todos/:id
DELETE /todos/:id
```

### Features

- Authentication (JWT)
    
- Pagination
    
- Filtering
    
- Sorting
    

Example

```
GET /todos?page=1&limit=10&status=pending
```

---

# 2. Design a URL Shortener (like Bitly)

You actually built something similar with **shortlyapp**, so this is perfect practice.

### Flow

```
User submits long URL
       ↓
Server generates short code
       ↓
Store in database
       ↓
Return short link
```

Example

```
POST /shorten
```

Request

```
{
 "url": "https://google.com"
}
```

Response

```
shortlyapp.in/aB3x9
```

### Database

```
{
 shortCode: "aB3x9",
 originalUrl: "...",
 clicks: 20,
 createdAt: Date
}
```

---

# 3. Design Authentication System

### Steps

```
Register
Login
Access protected routes
```

Flow

```
User login
   ↓
Server validates credentials
   ↓
Generate JWT token
   ↓
Client stores token
   ↓
Send token in Authorization header
```

Example

```
Authorization: Bearer TOKEN
```

Middleware verifies token.

---

# 4. Design a File Upload Service

Example: uploading profile pictures.

### Flow

```
Client uploads file
     ↓
Server receives file
     ↓
Store in cloud storage
     ↓
Save file URL in database
```

Technologies

- Multer (upload handling)
    
- AWS S3 / Cloudinary
    
- CDN for faster access
    

Example API

```
POST /upload
```

---

# 5. Design a Notification System

Example: notifications for comments.

### Components

```
User
Notification
Event system
```

Flow

```
User comments
     ↓
Event triggered
     ↓
Notification created
     ↓
Send to user
```

Possible technologies

- Redis
    
- WebSockets
    
- Message queues
    

---

# 6. Design Pagination System

Large datasets must not be returned all at once.

Example

```
GET /products?page=2&limit=10
```

Database query

```
skip = (page-1)*limit
```

Benefits

- Faster response
    
- Lower memory usage
    

---

# 7. Design Search Feature

Example

```
GET /products?q=laptop
```

Implementation

```
MongoDB text index
ElasticSearch
```

Example Mongo query

```
Product.find({ $text: { $search: "laptop" } })
```

---

# 8. Design Rate Limiting

Purpose: protect server from abuse.

Example

```
100 requests per minute
```

Implementation

```
IP tracking
Redis counters
```

Express example

```
express-rate-limit
```

---

# 9. Design Logging System

Logs help debugging.

Example logs

```
Request received
User login
Error occurred
```

Tools

- Winston
    
- Morgan
    
- ELK stack
    

Example

```
GET /todos → 200
POST /login → 401
```

---

# 10. Design API Security

Important for production systems.

Techniques

### Authentication

```
JWT tokens
OAuth
```

### Security middleware

```
Helmet
Rate limiting
CORS
```

### Password security

```
bcrypt hashing
```

---

# How to Answer System Design Questions

When interviewer asks:

> “Design X system”

Follow this structure.

### 1️⃣ Clarify requirements

Example

```
Should the system support millions of users?
Do we need authentication?
```

---

### 2️⃣ Define entities

Example

```
User
Todo
Activity
```

---

### 3️⃣ Define API endpoints

Example

```
GET /todos
POST /todos
```

---

### 4️⃣ Database design

Example

```
Todo
- title
- status
- userId
```

---

### 5️⃣ Scaling ideas

Mention things like

```
Caching
Load balancing
Indexing
Pagination
```

---

# Bonus: Very Common Junior Backend Interview Question

### “Explain your Todo project”

Your answer can look like this:

> I built a Todo API using Node.js, Express, and MongoDB.  
> It supports CRUD operations for tasks.  
> Authentication is handled using JWT tokens.  
> Middleware validates tokens before accessing protected routes.  
> Pagination and filtering are implemented for better performance.  
> Error handling middleware ensures consistent API responses.

That answer will sound **very professional**.

---

## One more thing that will help you a LOT

If you want, I can show you:

**"15 mistakes backend developers make in interviews"**

These mistakes cause **many good developers to fail interviews**, even if they know coding.

Great question to ask. Many developers know coding but still **lose interviews because of small mistakes**. If you avoid these, your chances increase a lot.

Below are **15 common mistakes backend developers make in interviews** and how you can avoid them.

---

# 1. Jumping to code too quickly

Many candidates immediately start writing code.

Interviewers prefer this approach:

1. Understand the problem
    
2. Explain the approach
    
3. Then write code
    

Good habit:

> “First I will explain my approach, then I will implement it.”

---

# 2. Not asking clarifying questions

Strong developers always ask questions.

Example:

- What is the expected input?
    
- What should we return if data is not found?
    
- Should the API support pagination?
    

This shows **thinking ability**.

---

# 3. Ignoring edge cases

Interviewers love edge cases.

Example for Todo API:

- What if todo does not exist?
    
- What if title is empty?
    
- What if user is unauthorized?
    

Always mention validation.

Example:

```javascript
if (!title) {
   return res.status(400).json({ message: "Title required" });
}
```

---

# 4. Not explaining your code

Do not silently type.

Explain while coding.

Example:

> “Here I am creating middleware to verify the JWT token.”

This shows **confidence and communication skill**.

---

# 5. Forgetting error handling

Many developers forget proper error handling.

Good backend code always handles errors.

Example:

```javascript
try {
   const todo = await Todo.findById(id);
} catch (err) {
   return res.status(500).json({ message: "Server error" });
}
```

Or using your approach with **asyncHandler**.

---

# 6. Returning wrong HTTP status codes

Interviewers sometimes check this.

Common ones:

|Status|Meaning|
|---|---|
|200|Success|
|201|Created|
|400|Bad request|
|401|Unauthorized|
|404|Not found|
|500|Server error|

Example:

```javascript
return res.status(201).json({ message: "Todo created" });
```

---

# 7. Poor API design

Bad example

```
/getAllTodos
/createTodo
/deleteTodo
```

Better REST style

```
GET /todos
POST /todos
DELETE /todos/:id
```

Always design **RESTful APIs**.

---

# 8. Ignoring security

Even junior developers should mention security.

Good things to mention:

- JWT authentication
    
- password hashing (bcrypt)
    
- rate limiting
    
- helmet middleware
    
- input validation
    

Example answer:

> “I would hash passwords using bcrypt before storing them.”

---

# 9. Not discussing scalability

Interviewers like when you mention **scalability ideas**.

Example improvements:

- pagination
    
- indexing
    
- caching
    
- load balancing
    

Example answer:

> “For large datasets I would implement pagination.”

---

# 10. Hardcoding secrets

Bad practice:

```javascript
const JWT_SECRET = "mysecret";
```

Good practice:

```javascript
process.env.JWT_SECRET
```

Always use **environment variables**.

---

# 11. Not validating inputs

Never trust user input.

Example validation

```javascript
if (!email || !password) {
   return res.status(400).json({ message: "Invalid input" });
}
```

Better tools:

- Joi
    
- Zod
    
- express-validator
    

---

# 12. Writing messy code

Good code should be **clean and modular**.

Bad example

```
Everything in one file
```

Better structure

```
routes/
controllers/
models/
middlewares/
utils/
```

---

# 13. Forgetting middleware power

Many beginners put everything inside controllers.

Better approach:

Use middleware for

- authentication
    
- validation
    
- logging
    

Example

```javascript
router.get("/todos", verifyToken, getTodos);
```

---

# 14. Not testing API

Interviewers sometimes ask:

> “How would you test this API?”

Good answers:

Tools

- Postman
    
- Thunder Client
    
- Curl
    
- Automated tests (Jest, Supertest)
    

Example

```
POST /todos
GET /todos
DELETE /todos/:id
```

---

# 15. Not explaining your project properly

You should always be able to explain:

1. Problem
    
2. Architecture
    
3. Features
    
4. Challenges
    
5. Improvements
    

Example answer:

> I built a Todo API using Node.js, Express, and MongoDB. It supports CRUD operations with authentication using JWT. Middleware validates tokens before protected routes. Pagination and filtering improve performance, and error handling middleware ensures consistent responses.

This type of explanation impresses interviewers.

---

# Extra Tip (Very Important)

When answering backend questions, try to mention these **four pillars**:

1️⃣ Security  
2️⃣ Performance  
3️⃣ Scalability  
4️⃣ Maintainability

Example answer:

> “To improve performance I would add indexing and pagination. For security I would use JWT authentication and bcrypt hashing.”

---

# One powerful interview trick

Before coding, say this:

> “First I will design the API, then implement the controller.”

Interviewers **love structured thinking**.

---

If you want, I can also show you something extremely useful:

**“How to explain your MERN Todo project in interviews (perfect answer)”**

This is something interviewers ask **very frequently.** It will help you sound much more confident.