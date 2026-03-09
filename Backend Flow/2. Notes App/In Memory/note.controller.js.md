# 🎮 CONTROLLER — IN-MEMORY (PSEUDOCODE)

```
START NoteController

FOR create request
    CALL service.create
    SEND response

FOR getAll request
    CALL service.getAll with query params
    SEND response

FOR getById request
    CALL service.getById
    IF null → send 404
    ELSE send note

FOR update request
    CALL service.update
    IF null → send 404
    ELSE send updated note

FOR delete request
    CALL service.delete
    IF false → send 404
    ELSE confirm deletion

END NoteController
```

💬

> “Controllers are thin. All logic lives in services.”

This controller is the **HTTP layer** of your app.  
Its job is simple:

- Receive request from **frontend**
    
- Extract data from **req.body / req.params / req.query**
    
- Call **NoteService**
    
- Send response back to **frontend**
    

So the main flow is:

```text
User → Frontend → Express Route → Controller → Service → In-memory DB → Controller → Frontend
```

Now let’s walk through **real practical examples for each method**.

---

# 1️⃣ Creating a Note

### User action (Frontend)

User fills a form:

```
Title: Learn Node
Content: Understand service layer
Tags: backend,node
```

Frontend sends:

```http
POST /notes
Content-Type: application/json
```

Body:

```json
{
  "title": "Learn Node",
  "content": "Understand service layer",
  "tags": ["backend", "node"]
}
```

---

### Step 1 — Express receives request

Inside Express:

```js
req.body
```

becomes:

```js
{
  title: "Learn Node",
  content: "Understand service layer",
  tags: ["backend","node"]
}
```

---

### Step 2 — Controller calls service

```js
const note = NoteService.create(req.body);
```

So the service receives:

```js
data = {
  title: "Learn Node",
  content: "Understand service layer",
  tags: ["backend","node"]
}
```

---

### Step 3 — Service stores note

Service creates a Note object and stores it in memory:

```js
notes = {
  "1": {
    id: "1",
    title: "Learn Node",
    content: "Understand service layer",
    tags: ["backend","node"],
    isDeleted: false
  }
}
```

---

### Step 4 — Controller sends response

```js
res.json({
  success: true,
  data: note
});
```

Frontend receives:

```json
{
  "success": true,
  "data": {
    "id": "1",
    "title": "Learn Node",
    "content": "Understand service layer"
  }
}
```

---

# 2️⃣ Getting All Notes

User opens **Notes list page**.

Frontend request:

```http
GET /notes
```

Controller runs:

```js
NoteService.getAll(req.query)
```

Since no filters were passed:

```js
req.query = {}
```

Service returns all non-deleted notes.

Example response:

```json
{
  "success": true,
  "data": [
    {
      "id": "1",
      "title": "Learn Node"
    }
  ]
}
```

---

# 3️⃣ Searching Notes

Frontend request:

```http
GET /notes?search=node
```

Now inside controller:

```js
req.query = { search: "node" }
```

Controller passes filters:

```js
NoteService.getAll(req.query)
```

Service performs search:

```js
n.title.includes("node")
```

Example database:

```
Learn Node
React Hooks
Docker Guide
```

Result returned:

```
Learn Node
```

Controller sends response.

---

# 4️⃣ Get Note by ID

User clicks a note.

Frontend request:

```http
GET /notes/1
```

Inside controller:

```js
req.params.id = "1"
```

Controller calls:

```js
NoteService.getById("1")
```

Service looks in memory DB:

```js
notes["1"]
```

If found:

```json
{
  "success": true,
  "data": {
    "id": "1",
    "title": "Learn Node"
  }
}
```

If not found:

```json
{
  "message": "Note not found"
}
```

---

# 5️⃣ Updating a Note

User edits note.

Frontend request:

```http
PATCH /notes/1
```

Body:

```json
{
  "title": "Learn Node deeply"
}
```

---

### Step 1 — Controller receives

```js
req.params.id = "1"
req.body = { title: "Learn Node deeply" }
```

Controller calls:

```js
NoteService.update("1", req.body)
```

---

### Step 2 — Service updates note

Before update:

```
title = "Learn Node"
```

After update:

```
title = "Learn Node deeply"
```

Version history stores previous state:

```js
versionHistory = [
  {
    title: "Learn Node",
    updatedAt: ...
  }
]
```

---

### Step 3 — Controller sends response

```json
{
  "success": true,
  "data": {
    "title": "Learn Node deeply"
  }
}
```

---

# 6️⃣ Deleting a Note

User deletes note.

Frontend request:

```http
DELETE /notes/1
```

Controller runs:

```js
NoteService.delete(req.params.id)
```

Service marks note:

```
isDeleted = true
```

Database becomes:

```js
notes = {
  "1": {
    title: "Learn Node deeply",
    isDeleted: true
  }
}
```

---

Controller returns:

```json
{
  "success": true,
  "message": "Note deleted"
}
```

Now the note **won’t appear in `getAll()` results**.

---

# Complete Data Flow

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
NoteService
   │
   ▼
notes{} in-memory storage
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

# Why this controller is clean

This controller follows a **good separation of responsibilities**:

|Layer|Responsibility|
|---|---|
|Controller|Handles HTTP request/response|
|Service|Business logic|
|Model|Data structure|
|Routes|API endpoints|

This pattern is used in many **real Node.js backend projects**.

---

💡 One small improvement idea for later:

Add **input validation** before calling the service.

Example:

```js
if (!req.body.title) {
  return res.status(400).json({ message: "Title required" });
}
```

This makes your API **safer and production-ready**.