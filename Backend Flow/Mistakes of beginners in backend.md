Great 👍 This is an important topic. Many MERN developers write code that **works**, but experienced engineers immediately notice some mistakes. Fixing these will make your backend code look much more **professional and interview-ready**.

Here are **3 common controller mistakes** and how to fix them.

---

# 1️⃣ No Proper Error Handling

### ❌ Common beginner code

```javascript
exports.getTodo = async (req, res) => {
  const todo = await Todo.findById(req.params.id);
  res.json(todo);
};
```

### Problem

If the database fails, your server may crash.

Also if the todo does not exist, the API still returns **200 OK**, which is wrong.

---

### ✅ Better version

```javascript
export const getTodo = asyncHandler(async (req, res) => {

  const todo = await Todo.findById(req.params.id);

  if (!todo) {
    throw new AppError("Todo not found", 404);
  }

  res.json({ data: todo });

});
```

Now your code:

✔ handles DB errors  
✔ handles missing data  
✔ sends proper HTTP status

---

# 2️⃣ Trusting `req.body` Completely

Many beginners directly insert request body into database.

### ❌ Risky code

```javascript
const todo = await Todo.create(req.body);
```

Someone could send:

```json
{
  "title": "Buy milk",
  "isAdmin": true,
  "role": "superadmin"
}
```

Now your database contains **unexpected fields**.

---

### ✅ Better practice

Pick only allowed fields.

```javascript
const { title, description } = req.body;

const todo = await Todo.create({
  title,
  description
});
```

This protects your database from **malicious input**.

---

# 3️⃣ Inconsistent API Responses

Beginners often return different response structures.

### ❌ Example

```javascript
res.json(todo)

res.json({todo})

res.json({data: todo})

res.json({success: true, todo})
```

Frontend developers hate this because they must handle **different formats everywhere**.

---

### ✅ Professional APIs use consistent structure

Example standard:

```javascript
res.status(200).json({
  success: true,
  data: todo
});
```

Or with metadata:

```javascript
res.status(200).json({
  success: true,
  data: todo,
  message: "Todo fetched successfully"
});
```

Now every API behaves the same.

---

# ⭐ Bonus Tip (Very Important)

Many beginners mix **business logic inside controllers**.

Bad example:

```javascript
exports.createTodo = async (req, res) => {

  const todo = await Todo.create(req.body);

  await Activity.create({
    todoId: todo._id,
    action: "create"
  });

  res.json(todo);
};
```

In large apps this logic should go into **services**.

Example structure:

```
controllers/
services/
models/
routes/
middlewares/
utils/
```

Controller:

```javascript
const todo = await TodoService.create(req.body);
```

Service handles:

- database
    
- activity logs
    
- validation
    

This makes your project **clean and scalable**.

---

# 🚀 One Small Challenge For You

Try writing a **professional Todo controller** with these 5 APIs:

1. createTodo
    
2. getTodo
    
3. getAllTodos
    
4. updateTodo
    
5. softDeleteTodo
    

If you want, I can also show you **how senior backend engineers design CRUD controllers in just ~60 lines of code**, which is a really cool pattern used in many startups.