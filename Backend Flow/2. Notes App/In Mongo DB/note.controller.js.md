# 🎮 CONTROLLER — MONGODB (ASYNC)

```
START AsyncNoteController

TRY
    CALL service
    SEND success response
CATCH error
    LOG error
    SEND 500 response

END AsyncNoteController
```

💬

> “Async controllers with try-catch prevent server crashes.”

Think of the **controller as the bridge between HTTP requests and your service logic**.

So the real flow is:

```
Frontend → Express Route → Controller → Service → MongoDB
                                     ↓
                              Response back
```

Let’s go through **real practical examples for each method**.

---

# 1️⃣ Create Note

## User action (Frontend)

User writes a note in the UI:

```
Title: Learn Express
Content: Understand controller-service pattern
Tags: backend,node
```

Frontend sends request:

```
POST /notes
```

Body:

```json
{
  "title": "Learn Express",
  "content": "Understand controller-service pattern",
  "tags": ["backend", "node"]
}
```

---

## Step 1: Express route triggers controller

Example route:

```javascript
router.post("/notes", NoteController.create);
```

Now the controller runs:

```javascript
static async create(req, res)
```

Inside controller:

```
req.body =
{
  title: "Learn Express",
  content: "Understand controller-service pattern",
  tags: ["backend","node"]
}
```

---

## Step 2: Controller calls service

```javascript
const note = await NoteService.create(req.body);
```

Controller **does not talk to MongoDB directly**.  
Instead it delegates the job to **NoteService**.

---

## Step 3: Service creates document

Inside service:

```
Note.create({
  title,
  content,
  tags
})
```

MongoDB stores:

```json
{
  "_id": "101",
  "title": "Learn Express",
  "content": "Understand controller-service pattern",
  "tags": ["backend", "node"],
  "isDeleted": false,
  "createdAt": "2026-03-09"
}
```

Service returns this object to controller.

---

## Step 4: Controller sends response

Controller runs:

```javascript
res.status(201).json({
  success: true,
  data: note
});
```

Frontend receives:

```json
{
  "success": true,
  "data": {
    "_id": "101",
    "title": "Learn Express",
    "content": "Understand controller-service pattern"
  }
}
```

UI updates.

---

# 2️⃣ Get All Notes

User opens **Notes List page**.

Frontend sends:

```
GET /notes?tag=backend&search=express
```

---

## Controller receives request

```
req.query =
{
  tag: "backend",
  search: "express"
}
```

Controller calls:

```javascript
NoteService.getAll(req.query)
```

---

## Service runs query

Service builds Mongo query:

```
isDeleted = false
tags = backend
search = express
```

MongoDB query becomes roughly:

```
Find notes where:
isDeleted = false
AND tags = backend
AND (title contains "express" OR content contains "express")
```

Example result:

```json
[
  {
    "title": "Learn Express",
    "tags": ["backend"]
  }
]
```

---

## Controller sends response

```json
{
  "success": true,
  "data": [...]
}
```

Frontend renders list of notes.

---

# 3️⃣ Get Note by ID

User clicks a note.

Frontend sends:

```
GET /notes/101
```

Controller runs:

```javascript
NoteService.getById(req.params.id)
```

```
req.params.id = "101"
```

Service queries MongoDB:

```
findOne({
 _id: "101",
 isDeleted: false
})
```

Result:

```json
{
  "_id": "101",
  "title": "Learn Express"
}
```

Controller sends:

```json
{
  "success": true,
  "data": {...}
}
```

If note doesn't exist:

```json
{
  "success": false,
  "message": "Note not found"
}
```

---

# 4️⃣ Update Note

User edits note.

Frontend sends:

```
PATCH /notes/101
```

Body:

```json
{
  "title": "Learn Express deeply"
}
```

Controller runs:

```javascript
NoteService.update(req.params.id, req.body)
```

Service:

1️⃣ Finds note  
2️⃣ Saves previous version to history  
3️⃣ Updates title  
4️⃣ Saves document

Database becomes:

```json
{
  "title": "Learn Express deeply",
  "versionHistory": [
    {
      "title": "Learn Express"
    }
  ]
}
```

Controller returns updated note.

---

# 5️⃣ Delete Note

User clicks delete.

Frontend sends:

```
DELETE /notes/101
```

Controller runs:

```javascript
const ok = await NoteService.delete(req.params.id)
```

Service does **soft delete**:

```
note.isDeleted = true
```

Database becomes:

```json
{
  "_id": "101",
  "title": "Learn Express deeply",
  "isDeleted": true
}
```

Controller returns:

```json
{
  "success": true,
  "message": "Note deleted"
}
```

---

# 🔁 Full Data Flow (Important)

```
User Action
   │
   ▼
Frontend HTTP Request
   │
   ▼
Express Route
   │
   ▼
Controller
   │
   ▼
Service Layer
   │
   ▼
Mongoose Model
   │
   ▼
MongoDB
   │
   ▼
Result returned
   │
   ▼
Controller Response
   │
   ▼
Frontend UI updated
```

---

# ⭐ Why this architecture is good

Your project follows a **clean layered architecture**.

```
controllers → handle HTTP
services → business logic
models → database schema
routes → API mapping
```

Benefits:

- easier debugging
    
- easier testing
    
- scalable for large apps
    
- clean separation of responsibilities
    

This pattern is very common in **professional Node.js backends**.

---

💡 One powerful improvement you can add later:

Create a **global error handler middleware** so you don’t need `try/catch` in every controller.

That will make your controller much **cleaner and production-level**.