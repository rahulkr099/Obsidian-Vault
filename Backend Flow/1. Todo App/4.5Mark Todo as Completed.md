## 2️⃣ Pseudocode — **Mark Todo as Completed**

```bash
START completeTodo

1.READ todo ID from request parameters

2.CREATE update object:
	add status
	capture completion timestamp

3.FIND todo by ID and UPDATE where:
	3(1)FIND todo
		- id
		- not soft deleted

	3(2)UPDATE todo
	    - set update object
	    - increment version by 1
	3(3)RETURN updated document

4.IF todo not found
    SEND 404 error
    STOP - return

5.CREATE LOG activity:
	- store todo id
    - action = "complete"
    - store update data

6.SEND updated todo in response

END completeTodo
```
Let’s walk through a **real practical example** of how the data flows when a user marks a todo as completed. This will make every step of the controller very clear.

---

# 1️⃣ Todo already exists in database

Suppose MongoDB has this todo:

```json
{
  "_id": "65fa9001",
  "title": "Finish backend API",
  "status": "pending",
  "version": 2,
  "softDelete": false,
  "createdAt": "2026-03-09T12:00:00Z"
}
```

User sees this task in the UI.

```
Finish backend API
Status: Pending
```

---

# 2️⃣ User action on frontend

User clicks a button:

```
✔ Mark as Complete
```

Frontend sends request:

```http
PATCH /todos/65fa9001/complete
```

So Express receives:

```javascript
req.params
```

```json
{
  "id": "65fa9001"
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
id = "65fa9001"
```

---

# 4️⃣ Controller prepares update data

Your code:

```javascript
const update = {
  status: "done",
  completedAt: new Date()
};
```

Example value:

```json
{
  "status": "done",
  "completedAt": "2026-03-09T16:20:00Z"
}
```

So the system knows:

- task is finished
    
- when it was completed
    

---

# 5️⃣ Database update query runs

Your query:

```javascript
Todo.findOneAndUpdate(
  { _id: id, softDelete: false },
  { $set: update, $inc: { version: 1 } },
  { new: true }
);
```

MongoDB internally runs something like:

```javascript
db.todos.findOneAndUpdate(
  {
    _id: "65fa9001",
    softDelete: false
  },
  {
    $set: {
      status: "done",
      completedAt: "2026-03-09T16:20:00Z"
    },
    $inc: {
      version: 1
    }
  }
)
```

---

# 6️⃣ Database document changes

Before update:

```json
{
  "_id": "65fa9001",
  "title": "Finish backend API",
  "status": "pending",
  "version": 2
}
```

After update:

```json
{
  "_id": "65fa9001",
  "title": "Finish backend API",
  "status": "done",
  "completedAt": "2026-03-09T16:20:00Z",
  "version": 3
}
```

Two things happened:

```
status → changed to done
version → increased from 2 → 3
```

---

# 7️⃣ Check if todo exists

Your code:

```javascript
if (!todo) return res.status(404).json({ error: "Not found" });
```

Two possibilities:

### Case A: Todo exists

Controller continues.

### Case B: Todo not found

Example situations:

- wrong ID
    
- todo was deleted
    
- todo does not exist
    

Response:

```json
{
  "error": "Not found"
}
```

---

# 8️⃣ Activity log is created

Your code:

```javascript
await Activity.create({
  todoId: todo._id,
  action: "complete",
  payload: update
});
```

Now a new record is stored in **Activity collection**.

Example:

```json
{
  "_id": "act123",
  "todoId": "65fa9001",
  "action": "complete",
  "payload": {
    "status": "done",
    "completedAt": "2026-03-09T16:20:00Z"
  }
}
```

Now your system has **history tracking**.

Example timeline later:

```
Todo created
Todo updated
Todo completed
```

---

# 9️⃣ Response sent to frontend

Your code:

```javascript
res.json({ data: todo });
```

Frontend receives:

```json
{
  "data": {
    "_id": "65fa9001",
    "title": "Finish backend API",
    "status": "done",
    "completedAt": "2026-03-09T16:20:00Z",
    "version": 3
  }
}
```

---

# 🔁 Full Data Flow

```
User clicks "Mark Complete"
        │
        ▼
Frontend sends PATCH /todos/65fa9001/complete
        │
        ▼
Express receives request
        │
        ▼
req.params.id extracted
        │
        ▼
MongoDB findOneAndUpdate() runs
        │
        ▼
status changed to "done"
version incremented
        │
        ▼
Activity log created
        │
        ▼
Updated todo returned to frontend
        │
        ▼
Frontend updates UI
```

---

# ⭐ Why this controller is good design

This pattern is used in **real production systems** because:

✔ status updates are atomic  
✔ version tracking prevents conflicts  
✔ activity logging keeps history  
✔ softDelete protection avoids modifying deleted data

---

💡 **Small improvement idea**

Prevent completing an already completed task.

Example:

```javascript
if (todo.status === "done") {
  return res.status(400).json({ error: "Todo already completed" });
}
```

This avoids unnecessary updates.

---

If you want, I can also show you **a very clean folder structure for this Todo API** (controllers, services, models, routes) that most **professional Node.js backends use in startups.**