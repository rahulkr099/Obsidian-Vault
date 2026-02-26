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

5.CREATE database 'query' using filters [search this line on net]

6.IF search text exists
	On 'query'
	   - APPLY text search on todos
	   - SORT results by search relevance

7.CONVERT sortBy string into sorting rules

8.On 'query'
	APPLY sorting('7')
    SKIP (page - 1) * limit (Pagination skip)
	LIMIT number of results (Pagination limit)

9. RUN query + parallel in parallel for performance
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
