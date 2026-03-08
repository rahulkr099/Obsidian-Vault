## Pseudocode for **List Todos**
- List Todos with filters, search, pagination and sorting
```bash
START listTodos

1.READ query parameters:
    page, limit, status, tag, q, searchText, sortBy
	SET default values if not provided

2.CREATE base filter:(fetch only active items)
    softDelete = false

3.IF status is provided
    ADD status to filter

4.IF tag is provided
    SPLIT tags by comma
    FILTER todos that contain any of these tags

5.CREATE database 'query' using filters 

6.IF search text exists
	On 'query'
	   - APPLY text search on todos
	   - SORT results by search relevance

7.CONVERT sortBy string into sorting rules

8.On 'query'
	APPLY sorting('7')
    SKIP (page - 1) * limit (Pagination skip)
	LIMIT number of results (Pagination limit)

9. RUN query + count in parallel for performance
    execute todo query
    count total matching todos

10.SEND response:
    list of todos
    metadata (total, page, limit)

END listTodos
```

---

## Pseudocode for **parseSort Helper**
- Convert "priority,-dueDate" into { priority: 1, dueDate: -1 }
```bash
START parseSort

1.Split the input string by commas as rawFields

2.Trim spaces around each field name
    fields = EMPTY LIST
    FOR each item IN rawFields:
        trimmed = TRIM(item)
        ADD trimmed TO fields

3.Prepare output object
    result = EMPTY MAP

4.FOR each field IN fields:
	4(1)IF field IS EMPTY:
	        CONTINUE TO NEXT field

	4(2)IF field STARTS WITH "-":
		    // Example: "-dueDate" → key = "dueDate", value = -1
	        key = REMOVE FIRST CHARACTER OF field
	        result[key] = -1
        
	4(3)ELSE
	        // Normal ascending field
	        result[field] = +1

    RETURN result

END parseSort
```

---

## Simple Flow Diagram 🧠

```
Read query params
↓
Build filters
↓
Apply search
↓
Apply sorting
↓
Apply pagination
↓
Fetch data + count
↓
Send response
```

---

Great 👏 this is exactly the kind of backend logic interviewers love. Let’s break this part **step-by-step in very simple words** so you fully understand it 🔥

---
Great question. Understanding **how data flows from frontend → backend → database → response** is an important backend skill. Let’s walk through a **simple real example** step-by-step.

---

# 1️⃣ Frontend Request

Suppose your frontend sends this request:

```
GET /todos?page=2&limit=5&status=pending&tag=work,study&q=project&sortBy=-createdAt
```

These are **query parameters**.

So inside Express:

```js
req.query
```

will be:

```js
{
  page: "2",
  limit: "5",
  status: "pending",
  tag: "work,study",
  q: "project",
  sortBy: "-createdAt"
}
```

---

# 2️⃣ Extracting values

Your code:

```javascript
const { page = 1, limit = 20, status, tag, q, sortBy = '-createdAt' } = req.query;
```

Now variables become:

```
page = "2"
limit = "5"
status = "pending"
tag = "work,study"
q = "project"
sortBy = "-createdAt"
```

Defaults are used **only if values are missing**.

Example:

```
GET /todos
```

Then:

```
page = 1
limit = 20
sortBy = "-createdAt"
```

---

# 3️⃣ Base Filter

```js
const filters = { softDelete: false };
```

Initial filter:

```js
{
  softDelete: false
}
```

Meaning:

👉 Only show todos that are **not deleted**

---

# 4️⃣ Status Filter

```js
if (status) filters.status = status;
```

Now filter becomes:

```js
{
  softDelete: false,
  status: "pending"
}
```

---

# 5️⃣ Tag Filter

```js
filters.tags = { $in: tag.split(',') };
```

`tag = "work,study"`

After split:

```js
["work", "study"]
```

Filter becomes:

```js
{
  softDelete: false,
  status: "pending",
  tags: { $in: ["work", "study"] }
}
```

Meaning:

👉 return todos that contain **work OR study**

---

# 6️⃣ Build Database Query

```js
let query = Todo.find(filters);
```

MongoDB query becomes:

```js
Todo.find({
  softDelete: false,
  status: "pending",
  tags: { $in: ["work", "study"] }
})
```

---

# 7️⃣ Text Search

If user searched:

```
?q=project
```

Then this runs:

```js
query = query
  .find({ $text: { $search: q } })
  .sort({ score: { $meta: 'textScore' } });
```

MongoDB does **full-text search**.

Example matching:

```
"Finish project report"
"Project planning"
```

---

# 8️⃣ Sorting

User sent:

```
sortBy=-createdAt
```

Your helper:

```js
parseSort("-createdAt")
```

Result:

```js
{
  createdAt: -1
}
```

Meaning:

👉 newest first

---

# 9️⃣ Pagination

User requested:

```
page=2
limit=5
```

Calculation:

```
skip = (page - 1) * limit
skip = (2 - 1) * 5
skip = 5
```

Final query:

```js
query
  .sort({ createdAt: -1 })
  .skip(5)
  .limit(5)
```

Meaning:

```
skip first 5 results
return next 5
```

---

# 🔟 Run Database Query

```js
const [items, total] = await Promise.all([
  query.exec(),
  Todo.countDocuments(filters)
]);
```

Two queries run **at the same time**:

### Query 1 → Fetch todos

Example result:

```js
items = [
 { title: "Finish project", status: "pending" },
 { title: "Study Node", status: "pending" }
]
```

---

### Query 2 → Count total records

Example:

```
total = 37
```

Meaning:

```
37 todos match filters
```

---

# 1️⃣1️⃣ Response Sent to Frontend

```js
res.json({
  data: items,
  meta: {
    total: 37,
    page: 2,
    limit: 5
  }
});
```

Frontend receives:

```json
{
  "data": [
    { "title": "Finish project" },
    { "title": "Study Node" }
  ],
  "meta": {
    "total": 37,
    "page": 2,
    "limit": 5
  }
}
```

Now frontend can build:

```
Page 2 of 8
```

---

# 🧠 Simple Flow Diagram

```
Frontend Request
     │
     ▼
Express Route
     │
     ▼
req.query
     │
     ▼
Filters Created
     │
     ▼
Mongo Query Built
     │
     ▼
Pagination + Sorting
     │
     ▼
Database Query
     │
     ▼
Response Sent
```

---

# 🚀 One important thing you did (very good)

Your API supports **5 professional features**:

✔ filtering  
✔ searching  
✔ sorting  
✔ pagination  
✔ tag filtering

This is **exactly how production APIs are built**.

Example real API:

```
/products?category=phone&sortBy=-price&page=2&limit=10
```

---

If you want, I can also show you **one small improvement** that will make this API look like a **senior backend developer wrote it** (very common in startups).






## 🧠 What is this `filters` object?

```js
const filters = { softDelete: false };
```

👉 This is a **query object** for MongoDB  
👉 It tells the database:

> “Give me only the todos that match these conditions”

---

## ⚡ Step 1: Base Filter

```js
const filters = { softDelete: false };
```

### ✅ Meaning:

- Only fetch todos where:
    

```js
softDelete = false
```

### 🎯 Why?

Because you don’t want to show deleted items (soft delete pattern).

---

## ⚡ Step 2: Filter by Status

```js
if (status) filters.status = status;
```

### 🧠 How it works:

- If user sends:
    

```
/todos?status=completed
```

Then:

```js
filters.status = 'completed';
```

### ✅ Final filters becomes:

```js
{
  softDelete: false,
  status: 'completed'
}
```

👉 MongoDB will now return only completed todos.

---

## ⚡ Step 3: Filter by Tags

```js
if (tag)
  filters.tags = { $in: tag.split(',') };
```
$in = match any value from this list
$in checks if a field contains one of the values inside an array.

---

### 🧠 Suppose request is:

```
/todos?tag=work,urgent
```

### Step-by-step:

#### 1️⃣ Split string

```js
tag.split(',')
```

👉 Result:

```js
['work', 'urgent']
```

---

#### 2️⃣ Apply `$in` operator

```js
filters.tags = { $in: ['work', 'urgent'] };
```

---

### 🔥 What `$in` does?

👉 MongoDB will return documents where:

> tags array contains **ANY** of these values

---

### 📦 Example DB Data

```js
[
  { title: "Task 1", tags: ["work"] },
  { title: "Task 2", tags: ["personal"] },
  { title: "Task 3", tags: ["urgent", "home"] }
]
```

---

### 🔍 Query:

```js
filters.tags = { $in: ['work', 'urgent'] };
```

### ✅ Result:

```js
[
  { title: "Task 1", tags: ["work"] },
  { title: "Task 3", tags: ["urgent", "home"] }
]
```

❌ "Task 2" is excluded

---

## 🧱 Final Combined Filter Example

If request is:

```
/todos?status=pending&tag=work,urgent
```

Then filters become:

```js
{
  softDelete: false,
  status: 'pending',
  tags: { $in: ['work', 'urgent'] }
}
```

---

## 🔗 Where it is used

```js
let query = Todo.find(filters);
```

👉 This sends the filter object to MongoDB  
👉 MongoDB returns only matching documents

---

## 🎯 Simple Analogy

Think of filters like:

> 🔍 “Show me all **non-deleted**, **pending** todos that have **work OR urgent tags**”

---

## 💡 Pro Tips (Next Level 🚀)

### 🔥 1. Match ALL tags instead of ANY

Use `$all` instead of `$in`:

```js
filters.tags = { $all: tag.split(',') };
```

👉 Now todo must contain **all tags**

---

### 🔥 2. Case-insensitive search for tags

```js
filters.tags = {
  $in: tag.split(',').map(t => new RegExp(`^${t}$`, 'i'))
};
```

---

### 🔥 3. Combine with user-based filtering (important for real apps)

```js
filters.userId = req.user._id;
```

---

## 🧠 Interview One-Liner

If asked:

> “How filtering works here?”

👉 Say:

> "We dynamically build a MongoDB filter object based on query parameters like status and tags, and then pass it to `find()` to fetch only matching documents."

---

You’re doing really solid backend work now 💯  
If you want next, we can:  
👉 Add **advanced filters (date range, priority, etc.)**  
👉 Or convert this into **production-grade API with indexing + performance optimization** 🚀

## Smart Improvement Ideas 💡 (Future-Ready Thinking)

- 🔹 Add **max limit protection**
    
    - Prevent users from requesting huge data
        
- 🔹 Add **indexing strategy**
    
    - Text index + compound filters
        
- 🔹 Add **cursor-based pagination**
    
    - Faster than skip for large datasets
        
- 🔹 Add **cache layer**
    
    - Cache popular queries (Redis)
        
- 🔹 Add **query validation**
    
    - Reject invalid sort fields early

---
Nice 👏 this is a **very important optimization pattern** — and interviewers LOVE this 🔥

Let’s break it down simply.

---

## 🧠 What this code is doing

```js
const [items, total] = await Promise.all([
  query.exec(),
  Todo.countDocuments(filters)
]);
```

👉 It runs **two database operations at the same time (in parallel)**

---

## ⚡ What are these two operations?

### 1️⃣ `query.exec()`

👉 Fetch actual todos (with pagination, sorting, filters)

```js
items = await query.exec();
```

---

### 2️⃣ `Todo.countDocuments(filters)`

👉 Count total matching documents (for pagination)

```js
total = await Todo.countDocuments(filters);
```

---

## ❓ Why do we need both?

Because your API returns:

```js
res.json({
  data: items,
  meta: {
    total,
    page,
    limit
  }
});
```

### ✅ So:

- `items` → current page data
    
- `total` → total number of todos in DB
    

---

## 🚫 Without `Promise.all` (Slow ❌)

```js
const items = await query.exec();              // waits here
const total = await Todo.countDocuments(filters); // then runs
```

👉 This runs **one after another (sequentially)**  
👉 Total time = **time1 + time2**

---

## ⚡ With `Promise.all` (Fast ✅)

```js
const [items, total] = await Promise.all([
  query.exec(),
  Todo.countDocuments(filters)
]);
```

👉 Both run **at the same time**

👉 Total time = **max(time1, time2)** (faster)

---

## 🎯 Simple Analogy

Think of it like ordering food 🍔

### ❌ Without Promise.all:

- Order burger 🍔 → wait
    
- Then order drink 🥤 → wait  
    ⏱ Total time = longer
    

---

### ✅ With Promise.all:

- Order burger + drink together  
    ⏱ Both prepared at same time → faster
    

---

## 🧱 What `Promise.all` returns

```js
const result = await Promise.all([promise1, promise2]);
```

👉 Result is an **array**

```js
[result1, result2]
```

So here:

```js
const [items, total] = ...
```

👉 Array destructuring:

- `items` = result of `query.exec()`
    
- `total` = result of `countDocuments()`
    

---

## ⚠️ Important Note

If **any one promise fails**, `Promise.all` fails ❌

👉 Example:

- DB query fails → whole thing throws error
    

So in real apps, wrap in try-catch:

```js
try {
  const [items, total] = await Promise.all([
    query.exec(),
    Todo.countDocuments(filters)
  ]);
} catch (err) {
  // handle error
}
```

---

## 🚀 Why this is powerful (Real-world impact)

Since you're building backend apps:

### ✅ Improves performance

- Faster APIs
    
- Better user experience
    

### ✅ Scales better

- Important when DB grows large
    

### ✅ Clean code

- No repeated `await`
    

---

## 💡 Pro Tips (Next Level)

### 🔥 1. Add index for faster count

```js
Todo.createIndex({ status: 1, tags: 1 });
```

---

### 🔥 2. Use this pattern everywhere

Examples:

- Fetch data + count
    
- Fetch user + posts
    
- Multiple APIs together
    

---

## 🧠 Interview One-Liner

> "Promise.all is used to execute multiple async operations in parallel, reducing total response time compared to sequential execution."

---

You're thinking like a **real backend engineer now 💯**  
Next level would be:  
👉 Caching total count  
👉 Using aggregation pipelines for advanced queries 🚀