## 4️⃣ Pseudocode — **Restore Soft-Deleted Todo**

```bash
START restoreTodo

1.READ todo ID from request parameters

2.FIND todo by ID and UPDATE where:
	2(1)FIND todo
		- id
	    - softDelete is true

	2(2)UPDATE todo:
	    - set softDelete = false
	    - increment version by 1
	      
2(3)RETURN updated document

3.IF todo not found
    SEND 404 
    error 'Not found or not deleted'
    STOP

4.CREATE LOG activity:
	- store todo id
    - action = "restore"
    - store payload as NULL

5.SEND restored todo in response

END restoreTodo
```
Let’s walk through a **real situation** where a previously deleted todo is restored. This will show how data flows through your controller.

---

# 1️⃣ A Todo exists but is soft-deleted

Suppose the database currently has this record:

```json
{
  "_id": "65fa9050",
  "title": "Practice DSA problems",
  "status": "pending",
  "softDelete": true,
  "version": 3,
  "createdAt": "2026-03-09T10:00:00Z"
}
```

Important part:

```
softDelete = true
```

That means the task is **hidden from normal todo lists** because your other APIs usually query:

```
softDelete: false
```

So the user cannot see this todo in the UI.

---

# 2️⃣ User opens “Deleted Tasks”

Many apps have something like:

```
Trash / Recently Deleted
```

User sees:

```
Practice DSA problems
[ Restore ]
```

When user clicks **Restore**, frontend sends request:

```http
PATCH /todos/65fa9050/restore
```

---

# 3️⃣ Express receives the request

Express extracts the route parameter.

```javascript
req.params
```

becomes:

```json
{
  "id": "65fa9050"
}
```

Your controller runs:

```javascript
const id = req.params.id;
```

Now:

```
id = "65fa9050"
```

---

# 4️⃣ Database update query runs

Your code:

```javascript
const todo = await Todo.findOneAndUpdate(
  { _id: id, softDelete: true },
  { $set: { softDelete: false }, $inc: { version: 1 } },
  { new: true }
);
```

MongoDB internally runs something like:

```javascript
db.todos.findOneAndUpdate(
  {
    _id: "65fa9050",
    softDelete: true
  },
  {
    $set: {
      softDelete: false
    },
    $inc: {
      version: 1
    }
  }
)
```

Meaning:

```
Find a deleted todo
and restore it
```

---

# 5️⃣ Database document changes

Before restore:

```json
{
  "_id": "65fa9050",
  "title": "Practice DSA problems",
  "softDelete": true,
  "version": 3
}
```

After restore:

```json
{
  "_id": "65fa9050",
  "title": "Practice DSA problems",
  "softDelete": false,
  "version": 4
}
```

Two things happened:

```
softDelete → true → false
version → 3 → 4
```

Now the todo becomes **visible again in the normal todo list**.

---

# 6️⃣ Check if todo exists

Your code:

```javascript
if (!todo)
  return res.status(404).json({ error: "Not found or not deleted" });
```

This happens if:

- ID is wrong
    
- todo never existed
    
- todo is **already active (not deleted)**
    

Example response:

```json
{
  "error": "Not found or not deleted"
}
```

---

# 7️⃣ Activity log is created

Your code:

```javascript
await Activity.create({
  todoId: todo._id,
  action: "restore",
  payload: null
});
```

Now a new activity record is saved.

Example:

```json
{
  "_id": "act890",
  "todoId": "65fa9050",
  "action": "restore",
  "payload": null,
  "createdAt": "2026-03-09T17:10:00Z"
}
```

Activity timeline becomes:

```
Todo created
Todo updated
Todo deleted
Todo restored
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
    "_id": "65fa9050",
    "title": "Practice DSA problems",
    "softDelete": false,
    "version": 4
  }
}
```

---

# 9️⃣ Frontend updates UI

Now the todo moves from:

```
Trash
```

back to

```
Active Tasks
```

User sees:

```
Practice DSA problems
Status: Pending
```

---

# 🔁 Full Data Flow

```
User clicks Restore
        │
        ▼
Frontend sends PATCH /todos/65fa9050/restore
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
softDelete changed to false
version incremented
        │
        ▼
Activity log created
        │
        ▼
Updated todo returned to frontend
        │
        ▼
Todo appears again in main list
```

---

# ⭐ Why this feature is useful

Soft delete + restore allows systems to:

```
Recover accidental deletions
Maintain audit history
Avoid permanent data loss
```

Many real systems work like this:

```
Google Drive Trash
Gmail Trash
Notion Deleted Pages
```

---

💡 **Nice architecture you built**

Your Todo API now supports a full lifecycle:

```
create
list
get
update
complete
delete (soft)
restore
activity tracking
```

That is actually **very close to how real production CRUD APIs are designed**.

---

If you want, I can also show you **one small architectural improvement** that will make this entire controller set look like it was written by a **senior backend engineer (service layer pattern)**.