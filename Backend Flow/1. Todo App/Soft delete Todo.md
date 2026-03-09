## 3️⃣ Pseudocode — **Soft Delete Todo**
- Soft delete (not removing document physically)
```bash
START softDeleteTodo

1.READ todo ID from request parameters

2.FIND todo by ID and UPDATE where:
	3(1)FIND todo
		- id
	    - not soft deleted

	3(2)UPDATE todo:
	    - set softDelete = true
	    - increment version by 1
	      
	3(3)RETURN updated document

4.IF todo not found
    SEND 404 error
    STOP

5.CREATE LOG activity:
	store todo Id
    action = "delete"
    store payload as NULL

6.SEND updated todo in response

END softDeleteTodo
```
Let’s walk through a **real situation** where a user deletes a todo from the app. This controller performs a **soft delete**, meaning the record stays in the database but is hidden from normal queries.

---

# 1️⃣ Existing Todo in Database

Assume MongoDB contains this todo:

```json
{
  "_id": "65fa9010",
  "title": "Prepare for interview",
  "status": "pending",
  "softDelete": false,
  "version": 1,
  "createdAt": "2026-03-09T11:30:00Z"
}
```

The task is visible in the user’s todo list.

---

# 2️⃣ User action on frontend

User clicks a button:

```
🗑 Delete Task
```

Frontend sends an HTTP request:

```http
DELETE /todos/65fa9010
```

Express receives this request.

Inside Express:

```javascript
req.params
```

becomes:

```json
{
  "id": "65fa9010"
}
```

---

# 3️⃣ Controller extracts the ID

Your code:

```javascript
const id = req.params.id;
```

Now:

```
id = "65fa9010"
```

---

# 4️⃣ Database update query runs

Your code:

```javascript
const todo = await Todo.findOneAndUpdate(
  { _id: id, softDelete: false },
  { $set: { softDelete: true }, $inc: { version: 1 } },
  { new: true }
);
```

MongoDB internally performs something like:

```javascript
db.todos.findOneAndUpdate(
  {
    _id: "65fa9010",
    softDelete: false
  },
  {
    $set: {
      softDelete: true
    },
    $inc: {
      version: 1
    }
  }
)
```

---

# 5️⃣ Database document changes

Before deletion:

```json
{
  "_id": "65fa9010",
  "title": "Prepare for interview",
  "softDelete": false,
  "version": 1
}
```

After soft delete:

```json
{
  "_id": "65fa9010",
  "title": "Prepare for interview",
  "softDelete": true,
  "version": 2
}
```

Two changes happened:

```
softDelete → false → true
version → 1 → 2
```

The document **still exists in MongoDB**, but your APIs usually filter with:

```
softDelete: false
```

So it disappears from the user interface.

---

# 6️⃣ Check if todo exists

Your code:

```javascript
if (!todo) return res.status(404).json({ error: "Not found" });
```

This triggers if:

- the ID is wrong
    
- the todo was already deleted
    
- the todo never existed
    

Example response:

```json
{
  "error": "Not found"
}
```

---

# 7️⃣ Activity log is created

Your code:

```javascript
await Activity.create({
  todoId: todo._id,
  action: "delete",
  payload: null
});
```

A new activity record is stored.

Example:

```json
{
  "_id": "act567",
  "todoId": "65fa9010",
  "action": "delete",
  "payload": null,
  "createdAt": "2026-03-09T16:40:00Z"
}
```

Now your system keeps **audit history**.

Example timeline later:

```
Todo created
Todo updated
Todo completed
Todo deleted
```

---

# 8️⃣ Response sent to frontend

Your code:

```javascript
res.json({ data: todo });
```

Frontend receives:

```json
{
  "data": {
    "_id": "65fa9010",
    "title": "Prepare for interview",
    "softDelete": true,
    "version": 2
  }
}
```

---

# 9️⃣ Frontend updates UI

Since `softDelete` is now `true`, the frontend usually removes it from the list.

User sees:

```
✔ Task removed from list
```

But the record still exists in the database.

---

# 🔁 Complete Data Flow

```
User clicks Delete
        │
        ▼
Frontend sends DELETE /todos/65fa9010
        │
        ▼
Express controller receives request
        │
        ▼
req.params.id extracted
        │
        ▼
MongoDB findOneAndUpdate()
        │
        ▼
softDelete set to true
version incremented
        │
        ▼
Activity log created
        │
        ▼
Response returned to frontend
        │
        ▼
Todo disappears from UI
```

---

# ⭐ Why soft delete is used in real systems

Many production systems use **soft delete instead of permanent deletion** because it allows:

- recovery of deleted data
    
- audit trails
    
- analytics
    
- legal compliance
    

Example:

```
Gmail Trash
Notion Deleted Pages
GitHub Deleted Repositories
```

They are usually **not permanently removed immediately**.

---

💡 **One powerful improvement idea**

Later you could implement:

```
POST /todos/:id/restore
```

Which simply sets:

```
softDelete = false
```

Now the todo comes back.

This makes your backend **much closer to real production APIs**.

---

If you'd like, I can also show you something very useful:  
how **all your controllers together form a complete REST API design**, the same structure used in many Node.js backend projects.