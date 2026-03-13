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