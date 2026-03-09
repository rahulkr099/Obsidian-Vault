## 1️⃣ Pseudocode — **Update Todo (Partial Update)**
- Update fields partially
- Version increments every update
```bash
START updateTodo

1.READ todo ID from request parameters
2.READ update data from request body as payload

3.FIND todo by ID to UPDATE where:
	3(1)FIND todo:
		    - id
			- not soft deleted
	3(2)UPDATE todo:
		    - set provided fields
		    - increment version by 1
	3(3)RETURN updated document

4.IF todo not found
    SEND 404 
    error "Not Found"
    STOP - RETURN 

5.CREATE LOG activity:
	- store todo ID
    - action = "update"
    - store payload

6.SEND updated todo in response

END updateTodo
```
Let’s walk through a **real example** so you can clearly see how the data moves from **frontend → backend → database → response**. Imagine you already have a todo stored in the database.

---

## 1. Existing Todo in Database

Example document in MongoDB:

```json
{
  "_id": "64ab21",
  "title": "Finish MERN project",
  "status": "pending",
  "priority": "medium",
  "version": 1,
  "softDelete": false
}
```

---

# Step-by-Step Flow

## 2. Frontend sends update request

User edits the task title in the UI.

Frontend sends:

```http
PATCH /todos/64ab21
Content-Type: application/json
```

Body:

```json
{
  "title": "Finish MERN backend project",
  "priority": "high"
}
```

---

## 3. Express receives the request

Inside Express:

```javascript
req.params
```

```json
{
  "id": "64ab21"
}
```

and

```javascript
req.body
```

```json
{
  "title": "Finish MERN backend project",
  "priority": "high"
}
```

---

## 4. Variables inside your controller

Your code:

```javascript
const id = req.params.id;
const payload = req.body;
```

Now values become:

```javascript
id = "64ab21"

payload = {
  title: "Finish MERN backend project",
  priority: "high"
}
```

---

## 5. Database Update Query

Your query:

```javascript
Todo.findOneAndUpdate(
  { _id: id, softDelete: false },
  { $set: payload, $inc: { version: 1 } },
  { new: true }
);
```

MongoDB internally runs something like:

```javascript
db.todos.findOneAndUpdate(
  {
    _id: "64ab21",
    softDelete: false
  },
  {
    $set: {
      title: "Finish MERN backend project",
      priority: "high"
    },
    $inc: {
      version: 1
    }
  }
)
```

---

## 6. What `$set` does

```javascript
$set: payload
```

means **update only the provided fields**.

Before update:

```json
{
  "title": "Finish MERN project",
  "priority": "medium"
}
```

After update:

```json
{
  "title": "Finish MERN backend project",
  "priority": "high"
}
```

Other fields remain unchanged.

---

## 7. What `$inc` does

```javascript
$inc: { version: 1 }
```

It increments the version.

Before:

```json
"version": 1
```

After:

```json
"version": 2
```

This is useful for:

- audit tracking
    
- concurrency control
    
- change history
    

---

## 8. `{ new: true }`

This option means:

Return the **updated document**, not the old one.

Returned todo:

```json
{
  "_id": "64ab21",
  "title": "Finish MERN backend project",
  "status": "pending",
  "priority": "high",
  "version": 2,
  "softDelete": false
}
```

---

## 9. Logging the activity

Your code logs the update:

```javascript
await Activity.create({
  todoId: todo._id,
  action: "update",
  payload
});
```

Activity collection will store:

```json
{
  "todoId": "64ab21",
  "action": "update",
  "payload": {
    "title": "Finish MERN backend project",
    "priority": "high"
  }
}
```

Now you have **history of changes**.

Example timeline:

```
Todo created
Todo updated
Todo completed
```

---

## 10. Response sent to frontend

```javascript
res.json({ data: todo });
```

Frontend receives:

```json
{
  "data": {
    "_id": "64ab21",
    "title": "Finish MERN backend project",
    "priority": "high",
    "version": 2
  }
}
```

Now the UI updates immediately.

---

# Full Flow (Simple Visual)

```
User edits todo
        │
        ▼
Frontend sends PATCH /todos/64ab21
        │
        ▼
Express receives request
        │
        ▼
req.params.id → "64ab21"
req.body → updated fields
        │
        ▼
MongoDB findOneAndUpdate()
        │
        ▼
Todo updated + version increased
        │
        ▼
Activity log created
        │
        ▼
Updated todo returned to frontend
```

---

## One smart thing in your code

This condition is very good:

```javascript
{ _id: id, softDelete: false }
```

It prevents updating **deleted todos**.

Many beginners forget this.

---

## Small improvement idea (very common in production)

Before updating, you can **validate allowed fields**.

Example:

```javascript
const allowed = ["title", "priority", "status"];
const payload = {};

allowed.forEach(field => {
  if (req.body[field] !== undefined) {
    payload[field] = req.body[field];
  }
});
```

This prevents users from updating things like:

```
version
createdAt
userId
```

---

If you want, I can also show you something **very important that many MERN developers don't understand properly**:

**Why `PATCH` is used for update instead of `PUT` in modern APIs.**  
That concept will make your API design much stronger.