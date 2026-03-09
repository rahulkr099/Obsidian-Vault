# 🧠 SERVICE LAYER — IN-MEMORY (CORE LOGIC)

### `note.service.js`

## Create Note

```
START createNote

CREATE new Note object using input data
STORE note in memory using note.id as key
RETURN created note

END createNote
```

---

## Get All Notes (Search + Filter)

```
START getAllNotes

FETCH all notes from memory
REMOVE notes where isDeleted = true

IF search query exists
    FILTER notes where title OR content contains query

IF tag filter exists
    FILTER notes that contain the tag

RETURN filtered notes list

END getAllNotes
```

---

## Get Note by ID

```
START getNoteById

FIND note using ID
IF note does not exist OR is deleted
    RETURN null

RETURN note

END getNoteById
```

---

## Update Note (With Versioning)

```
START updateNote

FIND note by ID
IF note does not exist OR is deleted
    RETURN null

SAVE current title and content into versionHistory

UPDATE provided fields only
UPDATE updatedAt timestamp

RETURN updated note

END updateNote
```

---

## Soft Delete Note

```
START deleteNote

FIND note by ID
IF note does not exist OR already deleted
    RETURN false

SET isDeleted = true
RETURN true

END deleteNote
```

💬

> “I used soft delete so data can be restored or audited later.”

This service layer is acting like a **mini database in memory**.  
Instead of MongoDB, you are storing notes inside this object:

```javascript
let notes = {};
```

Think of it like:

```
notes = {
   id1 → Note object
   id2 → Note object
}
```

Now let’s walk through **real practical examples** so the flow becomes clear.

---

# Overall Data Flow

In a typical Express app the flow looks like this:

```
Frontend Request
      │
      ▼
Controller
      │
      ▼
NoteService (this file)
      │
      ▼
notes {}  ← in-memory database
```

So this service is responsible for:

```
create
read
update
delete
search
filter
```

---

# 1️⃣ Creating a Note

### User Action

User fills a form:

```
Title: Learn Node
Content: Understand services
Tags: backend,node
```

Frontend sends:

```
POST /notes
```

Body:

```json
{
  "title": "Learn Node",
  "content": "Understand services",
  "tags": ["backend","node"]
}
```

---

### Controller calls service

```javascript
NoteService.create(req.body)
```

Inside service:

```javascript
const note = new Note(data.title, data.content, data.tags);
```

Suppose `Note` constructor generates:

```
id = "101"
```

New object created:

```javascript
{
  id: "101",
  title: "Learn Node",
  content: "Understand services",
  tags: ["backend","node"],
  isDeleted: false,
  versionHistory: []
}
```

---

### Stored in memory DB

```javascript
notes[note.id] = note;
```

Now memory DB becomes:

```javascript
notes = {
  "101": {
    id: "101",
    title: "Learn Node",
    content: "Understand services",
    tags: ["backend","node"]
  }
}
```

Service returns this note to controller → frontend.

---

# 2️⃣ Get All Notes

User opens **Notes list page**

Frontend sends:

```
GET /notes
```

Controller calls:

```javascript
NoteService.getAll(req.query)
```

---

### Step 1: Convert object → array

```javascript
Object.values(notes)
```

Result:

```javascript
[
  {
    id: "101",
    title: "Learn Node",
    content: "Understand services"
  }
]
```

---

### Step 2: Remove deleted notes

```javascript
.filter(n => !n.isDeleted)
```

Example:

```
Note1 → isDeleted = false ✔
Note2 → isDeleted = true ❌
```

So deleted notes disappear.

---

# 3️⃣ Searching Notes

Frontend request:

```
GET /notes?search=node
```

Now filter runs:

```javascript
n.title.toLowerCase().includes(q)
```

Example notes:

```
Learn Node
React Hooks
Docker Guide
```

Search query:

```
node
```

Result:

```
Learn Node
```

Because:

```
"learn node".includes("node") → true
```

---

# 4️⃣ Filtering by Tag

Frontend request:

```
GET /notes?tag=backend
```

Filter runs:

```javascript
n.tags.includes("backend")
```

Example notes:

```
Note1 tags: ["backend","node"]
Note2 tags: ["frontend"]
```

Result:

```
Note1
```

---

# 5️⃣ Get Note by ID

User opens a note page.

Frontend request:

```
GET /notes/101
```

Controller calls:

```javascript
NoteService.getById("101")
```

Service runs:

```javascript
const note = notes[id];
```

Which reads:

```
notes["101"]
```

If exists:

```javascript
{
  id: "101",
  title: "Learn Node"
}
```

Returned to controller.

---

# 6️⃣ Updating a Note

User edits note.

Frontend request:

```
PATCH /notes/101
```

Body:

```json
{
  "title": "Learn Node deeply"
}
```

Controller calls:

```javascript
NoteService.update("101", req.body)
```

---

### Step 1: Find note

```javascript
const note = notes[id];
```

---

### Step 2: Save version history

Before update:

```
title = Learn Node
```

Version history stores:

```javascript
note.versionHistory.push({
  title: "Learn Node",
  content: "Understand services",
  updatedAt: now
})
```

---

### Step 3: Update fields

```javascript
note.title = payload.title
```

Now note becomes:

```javascript
{
  id: "101",
  title: "Learn Node deeply",
  versionHistory: [
     { title: "Learn Node" }
  ]
}
```

---

# 7️⃣ Soft Delete

User deletes note.

Frontend request:

```
DELETE /notes/101
```

Controller calls:

```javascript
NoteService.delete("101")
```

Service runs:

```javascript
note.isDeleted = true
```

Now DB becomes:

```javascript
notes = {
  "101": {
    id: "101",
    title: "Learn Node deeply",
    isDeleted: true
  }
}
```

Note still exists but **will not appear in list queries**.

---

# Full Data Flow Example

```
User creates note
      │
      ▼
Controller receives request
      │
      ▼
NoteService.create()
      │
      ▼
notes{} object updated
      │
      ▼
Note returned to controller
      │
      ▼
Response sent to frontend
```

---

# Example Memory DB After Several Actions

```
notes = {

  "101": {
    title: "Learn Node deeply",
    tags: ["backend"],
    isDeleted: false
  },

  "102": {
    title: "React Basics",
    tags: ["frontend"],
    isDeleted: true
  }

}
```

Only note `101` will appear in list.

---

# Why this design is useful

This version helps you understand **backend logic before using MongoDB**.

It teaches core backend concepts:

```
CRUD operations
soft delete
search
filter
version history
service layer architecture
```

Exactly the same logic works when you switch to **MongoDB or Prisma**.

---

💡 A small improvement idea:

Right now search + filter runs **in memory**.

In real systems with databases, these operations happen **inside the database query** so the server doesn’t load thousands of records into memory.

---

If you want, I can also show you something very interesting:  
how **this in-memory service converts almost line-by-line into MongoDB code**, which helps understand backend development much faster.