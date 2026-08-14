# 🚀 curl Mastery Course

# Module 2 — Request Body

## 📚 Overview

In **Module 1**, you learned **how to ask a server for something**.

In **Module 2**, you'll learn **how to send data to the server**.

This is one of the most important modules because almost every backend API accepts data from clients.

Examples:

- User Registration
- User Login
- Create Todo
- Create Blog
- Update Profile
- Upload Image
- Send Payment Details

All of these require sending data in the **request body**.

---

# 🎯 Learning Objectives

By the end of this module, you'll be able to:

- Understand what a request body is.
- Send JSON data.
- Send nested JSON.
- Send arrays.
- Read request bodies from files.
- Send form data.
- Upload files.
- Debug request bodies using `httpbin` and Express.
- Understand how Express receives different body types.

---

# 📖 Module Roadmap

## Lesson 1 — What is a Request Body? ⭐⭐⭐⭐⭐

Learn:

- Request body vs headers vs URL
- Which HTTP methods support a body
- JSON fundamentals
- How servers read request bodies

Practice:

```bash
curl \
-X POST \
-H "Content-Type: application/json" \
-d '{"name":"Rahul"}' \
<https://httpbin.org/post>
```

---

## Lesson 2 — Sending JSON ⭐⭐⭐⭐⭐

Learn:

- `d`
- `-data`
- `-data-raw`
- `Content-Type`
- Strings
- Numbers
- Booleans
- Null

Practice:

```bash
curl \
-H "Content-Type: application/json" \
-d '{"age":21,"student":true}'
```

---

## Lesson 3 — Nested JSON ⭐⭐⭐⭐⭐

Learn:

Objects

```json
{
  "user":{
    "name":"Rahul",
    "age":21
  }
}
```

Arrays

```json
{
  "skills":[
    "JavaScript",
    "Node.js",
    "MongoDB"
  ]
}
```

Nested arrays

Objects inside arrays

Real API payloads

---

## Lesson 4 — Reading JSON from Files ⭐⭐⭐⭐☆

Instead of:

```bash
-d '{"name":"Rahul"}'
```

Use

```bash
-d @user.json
```

Learn:

- Why this is better
- Organizing API requests
- Reusable payloads

---

## Lesson 5 — Form Data ⭐⭐⭐⭐☆

Learn:

```
application/x-www-form-urlencoded
```

Practice:

```bash
curl \
-d "username=rahul&password=1234"
```

Compare with JSON.

---

## Lesson 6 — Multipart Form Data ⭐⭐⭐⭐⭐

Upload files

```bash
curl \
-F "image=@photo.jpg"
```

Upload multiple files

Mix text + files

---

## Lesson 7 — Express Request Body ⭐⭐⭐⭐⭐

Understand:

```jsx
req.body
```

Express middleware

```jsx
express.json()
```

```jsx
express.urlencoded()
```

How Express parses different body types.

---

## Lesson 8 — Debugging Request Bodies ⭐⭐⭐⭐⭐

Use:

```bash
-v
```

Use:

```bash
httpbin
```

Use:

```bash
jq
```

Find common mistakes:

- Invalid JSON
- Wrong Content-Type
- Missing body
- Empty body
- Incorrect quotes

---

## Lesson 9 — Real Backend Examples ⭐⭐⭐⭐⭐

Practice against an Express backend.

Register

```
POST /register
```

Login

```
POST /login
```

Create Todo

```
POST /todos
```

Update Todo

```
PATCH /todos/1
```

Delete Todo

```
DELETE /todos/1
```

---

## Lesson 10 — Mini Project ⭐⭐⭐⭐⭐

Build a complete API testing workflow using only:

- curl
- jq
- Bash
- Variables
- Functions

Exactly like Postman—but from the terminal.

---

# 🏁 Final Outcome

After this module, you'll be able to replace most day-to-day Postman usage with terminal commands for creating and updating resources, uploading files, and debugging request payloads.

---