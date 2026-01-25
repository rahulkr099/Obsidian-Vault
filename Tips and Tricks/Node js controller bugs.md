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

```php
Debug slow APIs step by step
```
Great question 👏  
**Debugging slow APIs is a top backend skill** — interviewers LOVE this, and real systems depend on it.  
Let’s go **step by step**, in **simple words**, exactly how a backend engineer thinks.

I’ll show:

- How to **find where time is going**
    
- Common **real causes**
    
- How to **fix each one**
    
- Smart ideas to **prevent slowness in future**
    

---

# 🐢 Step-by-Step: Debug a Slow API (Node.js + MongoDB)

---

## 🟢 STEP 1: Confirm it is REALLY slow

### Measure response time

```js
app.use((req, res, next) => {
  const start = Date.now();

  res.on("finish", () => {
    console.log(req.path, Date.now() - start, "ms");
  });

  next();
});
```

📌 Now you KNOW which API is slow

💡 Idea: Log anything > 500ms

---

## 🟢 STEP 2: Break API into parts (MOST IMPORTANT)

Add logs between steps:

```js
console.time("total");

console.time("db");
const user = await User.findById(id);
console.timeEnd("db");

console.time("logic");
// business logic
console.timeEnd("logic");

console.time("response");
res.send(user);
console.timeEnd("response");

console.timeEnd("total");
```

📌 This tells you **exactly what is slow**

---

## 🟡 STEP 3: Check database first (90% of cases)

### ❌ Very common slow code

```js
for (let id of ids) {
  await User.findById(id);
}
```

### ✅ Fix (Batch query)

```js
const users = await User.find({ _id: { $in: ids } });
```

💡 Idea: Always ask

> “Can this be done in ONE query?”

---

## 🟡 STEP 4: Missing indexes (huge slowdown)

### ❌ Query

```js
User.find({ email: "test@gmail.com" });
```

### ✅ Index

```js
db.users.createIndex({ email: 1 });
```

📌 Without index → full collection scan

💡 Interview line:

> “Indexes reduce query time from O(n) to O(log n)”

---

## 🟡 STEP 5: Fetching TOO much data

### ❌ Bad

```js
User.find();
```

### ✅ Good

```js
User.find().select("name email");
```

📌 Less data = faster network + memory

💡 Idea: Never return fields you don’t need

---

## 🟡 STEP 6: Using `populate()` blindly

### ❌ Slow

```js
Post.find().populate("author").populate("comments");
```

### ✅ Better

```js
Post.find()
  .populate("author", "name")
  .limit(10);
```

💡 Idea: Limit + select ALWAYS with populate

---

## 🟠 STEP 7: Blocking code (event loop stuck)

### ❌ Bug

```js
for (let i = 0; i < 1e9; i++) {}
```

### 😵 Why slow

- Blocks event loop
    
- All requests wait
    

---

### ✅ Fix

- Move heavy work to:
    
    - Worker thread
        
    - Queue (BullMQ)
        
    - Background job
        

💡 Idea: Node.js hates CPU-heavy work

---

## 🟠 STEP 8: External API call is slow

### ❌ Bug

```js
await axios.get("payment-api");
```

### ✅ Fix

```js
await axios.get("payment-api", { timeout: 3000 });
```

💡 Idea: Always set timeout + retry logic

---

## 🟠 STEP 9: No caching (repeat same work)

### ❌ Slow

```js
User.findById(id);
```

### ✅ Fast (Redis idea)

```js
cache.get(id) || User.findById(id);
```

📌 Cache hot data

💡 Innovative idea:

- Cache at controller level
    
- Expire after 5 minutes
    

---

## 🔴 STEP 10: Too many requests (rate limit)

### Fix

```js
app.use(rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 100
}));
```

💡 Prevent abuse before scaling DB

---

## 🧠 GOLDEN DEBUG FLOW (Memorize this)

1️⃣ Measure time  
2️⃣ Add logs  
3️⃣ Check DB query  
4️⃣ Check index  
5️⃣ Reduce data  
6️⃣ Avoid loops + await  
7️⃣ Add cache  
8️⃣ Handle external calls

---

## 🚀 Real Interview Example Answer

**Q:** “How do you debug a slow API?”

**Answer (short & strong):**

> “I first measure total response time, then log each step.  
> I check database queries, missing indexes, large payloads, and loops with await.  
> Then I optimize queries, add caching, and ensure no blocking code runs on the event loop.”

---

## 🔥 Practice Challenge (Try this)

```js
app.get("/orders", async (req, res) => {
  const users = await User.find();
  for (let u of users) {
    u.orders = await Order.find({ userId: u._id });
  }
  res.send(users);
});
```

👉 Problems:

- N+1 queries
    
- Missing limit
    
- No select
    
- No index on `userId`
    

---

## 🌱 Next powerful upgrades for you

- MongoDB `explain()` deep dive
    
- Redis caching patterns
    
- Production logging strategy
    
- API load testing
    
- System design: scaling slow APIs
    

Tell me what you want next — we’ll make you **backend-interview ready** 💪🚀

```php
Build production error handler
```
Excellent choice 👍  
A **production-ready error handler** is what separates a **student project** from a **real backend system**.  
Let’s build it **step by step**, in **simple words**, and in a way you can **reuse in every MERN project**.

I’ll show:

- Clean folder structure
    
- Custom error class
    
- Global error middleware
    
- Async error handling
    
- Logging strategy
    
- Production vs development behavior
    
- Smart improvements (real-world ideas)
    

---

# 🏗️ Production Error Handler (Node.js + Express)

---

## 🟢 STEP 1: Create a custom Error class

📁 `utils/AppError.js`

```js
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);

    this.statusCode = statusCode;
    this.status = `${statusCode}`.startsWith("4") ? "fail" : "error";
    this.isOperational = true;

    Error.captureStackTrace(this, this.constructor);
  }
}

module.exports = AppError;
```

📌 Why?

- Distinguish **expected errors** vs **bugs**
    
- Clean error structure
    

---

## 🟢 STEP 2: Async error wrapper (VERY IMPORTANT)

📁 `utils/catchAsync.js`

```js
module.exports = fn => {
  return (req, res, next) => {
    fn(req, res, next).catch(next);
  };
};
```

📌 No more try/catch everywhere 🎉

---

## 🟢 STEP 3: Use errors in controllers

📁 `controllers/userController.js`

```js
const AppError = require("../utils/AppError");
const catchAsync = require("../utils/catchAsync");

exports.getUser = catchAsync(async (req, res, next) => {
  const user = await User.findById(req.params.id);

  if (!user) {
    return next(new AppError("User not found", 404));
  }

  res.status(200).json({
    status: "success",
    data: user
  });
});
```

📌 Business logic stays clean

---

## 🟢 STEP 4: Global error handling middleware

📁 `middlewares/errorHandler.js`

```js
const AppError = require("../utils/AppError");

module.exports = (err, req, res, next) => {
  err.statusCode = err.statusCode || 500;
  err.status = err.status || "error";

  if (process.env.NODE_ENV === "development") {
    res.status(err.statusCode).json({
      status: err.status,
      message: err.message,
      stack: err.stack
    });
  } else {
    // Production
    if (err.isOperational) {
      res.status(err.statusCode).json({
        status: err.status,
        message: err.message
      });
    } else {
      console.error("💥 UNEXPECTED ERROR", err);

      res.status(500).json({
        status: "error",
        message: "Something went wrong"
      });
    }
  }
};
```

📌 Users never see stack trace in production

---

## 🟢 STEP 5: Handle unknown routes

📁 `app.js`

```js
const AppError = require("./utils/AppError");

app.all("*", (req, res, next) => {
  next(new AppError(`Can't find ${req.originalUrl}`, 404));
});
```

📌 Prevent silent failures

---

## 🟢 STEP 6: Plug error middleware LAST

📁 `app.js`

```js
const globalErrorHandler = require("./middlewares/errorHandler");

app.use(globalErrorHandler);
```

📌 Order matters 🔥

---

## 🟡 STEP 7: Handle MongoDB errors nicely

📁 `middlewares/errorHandler.js`

```js
const handleCastErrorDB = err =>
  new AppError("Invalid ID format", 400);

const handleDuplicateFieldsDB = err =>
  new AppError("Duplicate field value", 400);

const handleValidationErrorDB = err =>
  new AppError(err.message, 400);
```

Use inside production block:

```js
if (err.name === "CastError") err = handleCastErrorDB(err);
if (err.code === 11000) err = handleDuplicateFieldsDB(err);
if (err.name === "ValidationError") err = handleValidationErrorDB(err);
```

📌 Clean DB messages for frontend

---

## 🟡 STEP 8: Handle JWT errors

```js
if (err.name === "JsonWebTokenError") {
  err = new AppError("Invalid token", 401);
}

if (err.name === "TokenExpiredError") {
  err = new AppError("Token expired", 401);
}
```

📌 Auth errors become user-friendly

---

## 🔵 STEP 9: Central logging (production idea)

```js
if (!err.isOperational) {
  // Send to logger service
  // winston / pino / cloud logging
}
```

💡 Innovative idea:

- Log error + request ID
    
- Track user ID if available
    

---

## 🧠 Final Folder Structure (Clean MVC)

```
src/
 ├── controllers/
 ├── middlewares/
 │    └── errorHandler.js
 ├── utils/
 │    ├── AppError.js
 │    └── catchAsync.js
 ├── routes/
 ├── models/
 └── app.js
```

---

## 🧪 Test This Setup (Must-do)

Test these cases:

- Invalid ID
    
- Missing route
    
- DB validation error
    
- Auth error
    
- Unknown crash
    

---

## 🚀 Interview Answer (Perfect)

**Q:** How do you handle errors in production?

**Answer:**

> “I use a global error handler with a custom error class.  
> I separate operational errors from programming errors,  
> hide stack traces in production, and centralize logging.”

---

## 🌱 Powerful Next Improvements (Future-ready)

- Add request correlation ID
    
- Error retry strategy
    
- Graceful shutdown on crash
    
- Structured logs (JSON)
    
- Monitoring alerts
    

If you want, next we can:

- Add **Winston/Pino logging**
    
- Build **graceful shutdown**
    
- Handle **background job errors**
    
- Design **enterprise-level backend template**
    

Just say the word 🚀

```php
API load testing
```

Awesome 👍  
**API load testing** is how you prove your backend can handle **real users**, not just happy-path tests.  
I’ll explain it **step by step**, in **simple words**, with **real commands**, **real thinking**, and **production tips**.

---

# 🚦 What is API Load Testing? (Simple)

👉 Load testing means:

- Sending **many requests at the same time**
    
- Checking **speed**, **errors**, and **stability**
    
- Finding the **breaking point** before users do
    

Think like this:

> “What happens if 1,000 users hit my API together?”

---

# 🧠 When should you load test?

You SHOULD load test when:

- API feels slow sometimes
    
- Before production release
    
- Before interviews (huge plus)
    
- After DB or cache changes
    
- Before scaling
    

---

# 🧪 Key metrics you must watch

During load testing, focus on:

1️⃣ **Response time** (avg, p95, p99)  
2️⃣ **Throughput** (req/sec)  
3️⃣ **Error rate** (timeouts, 500s)  
4️⃣ **CPU & memory**  
5️⃣ **DB performance**

💡 Interview tip:

> “p95 latency matters more than average”

---

# 🛠️ Tool 1: Autocannon (BEST for Node.js)

### Install

```bash
npm install -g autocannon
```

### Basic test

```bash
autocannon -c 100 -d 20 http://localhost:3000/api/users
```

Meaning:

- `-c 100` → 100 concurrent users
    
- `-d 20` → 20 seconds test
    

---

### Sample output (how to read)

```
Latency avg: 120 ms
Latency p95: 300 ms
Requests/sec: 850
Errors: 0
```

📌 p95 = 95% users got response under 300ms → GOOD

---

# 🛠️ Tool 2: Postman (Beginner-friendly)

Postman → Collection → **Runner**

- Set iterations (100–1000)
    
- Add delay (optional)
    
- Watch response time graph
    

⚠️ Not true load testing, but good start

---

# 🛠️ Tool 3: k6 (Industry-level)

### Install

```bash
brew install k6
# or
sudo apt install k6
```

### Test script

```js
import http from "k6/http";
import { sleep } from "k6";

export let options = {
  vus: 100,
  duration: "30s",
};

export default function () {
  http.get("http://localhost:3000/api/users");
  sleep(1);
}
```

### Run

```bash
k6 run test.js
```

💡 k6 is GREAT for resumes and interviews

---

# 🔍 Step-by-Step: How to debug load test results

---

## 🟢 STEP 1: Is response time growing?

If:

- 1 user → 100ms
    
- 100 users → 2000ms ❌
    

👉 Something is blocking or DB is slow

---

## 🟡 STEP 2: Check error rate

Errors like:

- 500 → server bug
    
- 429 → rate limit
    
- Timeout → DB or external API
    

👉 Fix errors before scaling

---

## 🟡 STEP 3: CPU at 100%?

Cause:

- Heavy loops
    
- JSON parsing
    
- Encryption
    
- Sync code
    

Fix:

- Move work to background
    
- Cache
    
- Optimize logic
    

---

## 🟡 STEP 4: DB is bottleneck (MOST COMMON)

Signs:

- Slow queries
    
- High response time
    
- Low CPU but slow API
    

Fix:

- Add indexes
    
- Reduce payload
    
- Avoid N+1 queries
    
- Use cache (Redis)
    

---

## 🟠 STEP 5: External API calls

Bad pattern:

```js
await paymentAPI();
```

Under load → disaster 😵

Fix:

- Timeout
    
- Retry
    
- Circuit breaker
    
- Async queue
    

---

# 🚀 Load Testing a REAL API (Example)

### API

```http
GET /api/orders
```

### Test

```bash
autocannon -c 200 -d 30 http://localhost:3000/api/orders
```

### Result

- p95 = 2.5s ❌
    

### Fix applied

- Index on `userId`
    
- Added Redis cache
    
- Limited response fields
    

### Result after fix

- p95 = 300ms ✅
    

🔥 That’s a production story

---

# 🧠 Golden Load Testing Strategy (Memorize)

1️⃣ Test with small load  
2️⃣ Increase gradually  
3️⃣ Find breaking point  
4️⃣ Fix bottleneck  
5️⃣ Test again  
6️⃣ Document results

---

# 🎤 Interview-ready answer (Strong)

**Q: How do you load test APIs?**

**Answer:**

> “I use tools like autocannon or k6 to simulate concurrent users.  
> I track p95 latency, error rate, and throughput.  
> If performance drops, I inspect DB queries, indexes, caching, and blocking code.”

---

# 🌱 Smart Improvements (Advanced ideas)

- Add request IDs to trace slow calls
    
- Separate read & write DB
    
- Add Redis caching
    
- Add rate limiting
    
- Use horizontal scaling
    

---

# 🧪 Mini Practice Challenge for you

Imagine this API:

```js
app.get("/products", async (req, res) => {
  const products = await Product.find();
  res.send(products);
});
```

Under load, it’s slow.  
👉 How would YOU fix it?

(Hint: limit, index, cache, select)

---

If you want next, we can:

- Load test **MongoDB aggregation**
    
- Test **JWT auth APIs**
    
- Compare **Redis vs DB under load**
    
- Simulate **10k users**
    
- Prepare **system design performance answers**
    

Just tell me 🚀