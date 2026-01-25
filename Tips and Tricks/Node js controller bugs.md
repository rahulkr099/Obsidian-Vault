Perfect 👍  
**Node.js controller bugs are VERY common** in interviews and real backend work.  
Let’s debug **real bugs you’ll actually face**, in **simple words**, step by step.

I’ll show:

- ❌ Buggy controller code
    
- 😵 Why it breaks
    
- ✅ Fixed code
    
- 💡 Backend best-practice tip
    

---

## 🐞 BUG 1: `this` is undefined in controller method

### ❌ Buggy code

```js
class UserController {
  getProfile(req, res) {
    res.send(this.service.getUser());
  }
}

module.exports = new UserController();
```

### 😵 Why it breaks

- Route passes function reference
    
- `this` is lost
    

---

### ✅ Fix: Arrow function

```js
class UserController {
  getProfile = (req, res) => {
    res.send(this.service.getUser());
  };
}
```

💡 **Rule**: Controller methods → arrow functions

---

## 🐞 BUG 2: Response sent twice (CRASH)

### ❌ Buggy code

```js
app.get("/user", async (req, res) => {
  if (!req.user) {
    res.status(401).send("Unauthorized");
  }

  res.send("Welcome");
});
```

### 😵 Why it breaks

- Code continues after sending response
    
- Node throws error: _Cannot set headers_
    

---

### ✅ Fix: `return`

```js
if (!req.user) {
  return res.status(401).send("Unauthorized");
}
```

💡 **Rule**: Always `return` after `res.send()`

---

## 🐞 BUG 3: Async error not caught (server crashes)

### ❌ Buggy code

```js
app.get("/data", async (req, res) => {
  const data = await fetchData(); // throws error
  res.send(data);
});
```

### 😵 Why it breaks

- Unhandled promise rejection
    
- Server crashes
    

---

### ✅ Fix: `try/catch`

```js
try {
  const data = await fetchData();
  res.send(data);
} catch (err) {
  res.status(500).send("Server error");
}
```

💡 **Rule**: Every async controller needs error handling

---

## 🐞 BUG 4: Forgot `await` (undefined data)

### ❌ Buggy code

```js
const user = User.findById(req.params.id);
res.send(user);
```

### 😵 Why it breaks

- `user` is a Promise
    
- Response sends empty object
    

---

### ✅ Fix

```js
const user = await User.findById(req.params.id);
res.send(user);
```

💡 **Rule**: DB call → always `await`

---

## 🐞 BUG 5: Hanging request (no response)

### ❌ Buggy code

```js
app.get("/test", (req, res) => {
  if (req.query.ok) {
    res.send("OK");
  }
});
```

### 😵 Why it breaks

- If `ok` not present
    
- Request never ends
    

---

### ✅ Fix

```js
if (!req.query.ok) {
  return res.status(400).send("Missing param");
}
```

💡 **Rule**: Every path must send a response

---

## 🐞 BUG 6: Using `res.json` + `next()` together

### ❌ Buggy code

```js
app.get("/user", (req, res, next) => {
  res.json({ user: req.user });
  next();
});
```

### 😵 Why it breaks

- `next()` runs after response
    
- Middleware chain continues wrongly
    

---

### ✅ Fix

```js
return res.json({ user: req.user });
```

💡 **Rule**: Use `next()` OR send response — not both

---

## 🐞 BUG 7: Middleware order wrong (auth fails)

### ❌ Buggy code

```js
app.get("/profile", getProfile, authMiddleware);
```

### 😵 Why it breaks

- Profile runs before auth
    

---

### ✅ Fix

```js
app.get("/profile", authMiddleware, getProfile);
```

💡 **Rule**: Middlewares run left → right

---

## 🐞 BUG 8: `req.body` is undefined

### ❌ Buggy code

```js
app.post("/login", (req, res) => {
  console.log(req.body.username);
});
```

### 😵 Why it breaks

- Body parser missing
    

---

### ✅ Fix

```js
app.use(express.json());
```

💡 **Rule**: Always enable body parser

---

## 🐞 BUG 9: Mongoose validation ignored

### ❌ Buggy code

```js
User.updateOne({ _id: id }, data);
```

### 😵 Why it breaks

- Validators NOT run
    

---

### ✅ Fix

```js
User.updateOne({ _id: id }, data, { runValidators: true });
```

💡 **Rule**: Updates skip validation by default

---

## 🧠 CONTROLLER DEBUGGING CHECKLIST (Very useful)

Before blaming DB or frontend, check:

✔ `await` used  
✔ `return res.send()`  
✔ try/catch present  
✔ `this` bound correctly  
✔ Middleware order  
✔ Response sent exactly once

---

## 🚀 Practice Debug Task (Try this)

```js
app.get("/user/:id", async (req, res) => {
  const user = User.findById(req.params.id);
  if (!user) {
    res.status(404).send("Not found");
  }
  res.send(user);
});
```

👉 Bugs:

1. Missing `await`
    
2. Missing `return`
    

---

## 🔥 Next level ideas for you

- Debug **slow APIs step by step**
    
- Real **MongoDB controller traps**
    
- Build **production error handler**
    
- Machine-coding controller patterns
    
- Write **clean MVC folder structure**
    

Tell me what you want next and we’ll sharpen your backend skills fast 💪🚀

