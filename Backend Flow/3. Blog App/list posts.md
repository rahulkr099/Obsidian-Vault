Great practice 👍  
Turning controllers into **pseudocode** helps you understand the logic clearly. Let’s convert your `list` controller into simple step-by-step pseudocode.

---

# Pseudocode: List Posts with Pagination, Search, and Filtering

```text
FUNCTION listPosts(request, response, next)

    TRY

        // Step 1: Get pagination values from query parameters
        paginationData = getPagination(request.query)

        page  = paginationData.page
        limit = paginationData.limit
        skip  = paginationData.skip


        // Step 2: Create base filter condition
        filterQuery = { isDeleted : false }


        // Step 3: Apply full-text search if search query exists
        IF request.query.q exists THEN
            filterQuery.$text = { $search : request.query.q }
        ENDIF


        // Step 4: Apply tag filtering if tag exists
        IF request.query.tag exists THEN
            filterQuery.tags = lowercase(request.query.tag)
        ENDIF


        // Step 5: Run database queries in parallel

        totalPosts = count documents in Post collection
                     matching filterQuery

        posts = find posts in Post collection
                matching filterQuery
                sort by createdAt descending
                skip number of records (skip)
                limit number of records (limit)
                populate author fields (name, email)


        // Step 6: Build pagination metadata
        metadata = buildMeta(totalPosts, page, limit)


        // Step 7: Send response
        SEND response with:
            data = posts
            meta = metadata


    CATCH error
        PASS error to next middleware

END FUNCTION
```

---

# Simplified Logical Flow

```
Client Request
     ↓
Read query parameters
(page, limit, search, tag)
     ↓
Create filter query
     ↓
Add search condition if needed
     ↓
Add tag filter if needed
     ↓
Count total matching posts
     ↓
Fetch posts with pagination
     ↓
Attach author information
     ↓
Build pagination metadata
     ↓
Send response
```

---

# Example Request

```
GET /api/posts?page=1&limit=5&q=node&tag=backend
```

### What happens internally

Filter becomes:

```
{
  isDeleted: false,
  $text: { $search: "node" },
  tags: "backend"
}
```

Database then returns:

```
Newest 5 posts
matching search + tag
```

---

# Response Example

```json
{
  "data": [
    {
      "title": "Learning Node",
      "tags": ["backend","node"],
      "author": {
        "name": "Rahul",
        "email": "rahul@mail.com"
      }
    }
  ],
  "meta": {
    "page": 1,
    "limit": 5,
    "totalPages": 4,
    "totalItems": 20
  }
}
```

---

# A Small Backend Design Insight

This controller is doing **four backend tasks together**:

1. Pagination
    
2. Searching
    
3. Filtering
    
4. Metadata generation
    

This is a **very common pattern in production APIs**.

---

If you'd like, I can also show you something extremely useful for backend interviews and real projects:

**How big backend systems design this as:**

```
Controller
   ↓
Service
   ↓
Repository / Model
```

This pattern makes APIs **much cleaner and scalable**, and many startups expect this structure.

Let’s walk through a **real practical scenario** so you clearly see **how data flows step-by-step** in this controller.

Imagine your **blog API** is already running.

---

# 1. Client Sends Request

A user opens your frontend and searches posts.

**HTTP Request**

```
GET /api/posts?page=1&limit=3&q=node&tag=backend
```

Meaning:

|Parameter|Meaning|
|---|---|
|page=1|first page|
|limit=3|show 3 posts per page|
|q=node|search posts containing "node"|
|tag=backend|filter posts with tag "backend"|

---

# 2. Request Reaches Express Route

Example route:

```javascript
router.get("/posts", postController.list);
```

Flow becomes:

```
Client
   ↓
Express Router
   ↓
Controller (list)
```

Now the controller receives:

```javascript
req.query = {
  page: "1",
  limit: "3",
  q: "node",
  tag: "backend"
}
```

---

# 3. Pagination Calculation

Controller calls:

```javascript
const { page, limit, skip } = getPagination(req.query);
```

Example logic inside `getPagination`:

```
page = 1
limit = 3
skip = (page - 1) * limit
skip = 0
```

So we get:

```
page = 1
limit = 3
skip = 0
```

---

# 4. Base Filter Query

Controller creates a filter:

```javascript
const q = { isDeleted: false };
```

Meaning:

```
Only fetch posts that are NOT deleted
```

---

# 5. Add Search Condition

Since request contains:

```
q=node
```

Controller adds:

```javascript
q.$text = { $search: "node" }
```

Now filter becomes:

```
{
  isDeleted: false,
  $text: { $search: "node" }
}
```

MongoDB will search **text index fields** like title or content.

---

# 6. Add Tag Filter

Since request contains:

```
tag=backend
```

Controller adds:

```javascript
q.tags = "backend"
```

Final filter becomes:

```
{
  isDeleted: false,
  $text: { $search: "node" },
  tags: "backend"
}
```

Meaning:

```
Find posts:
- not deleted
- containing word "node"
- having tag "backend"
```

---

# 7. Database Queries Run in Parallel

Controller runs:

```javascript
Promise.all([
  Post.countDocuments(q),
  Post.find(q)...
])
```

Two queries run **at the same time**.

---

## Query 1 — Count Total Posts

MongoDB checks collection:

Example database:

```
posts collection
```

|title|tags|isDeleted|
|---|---|---|
|Node API Guide|backend,node|false|
|Node Performance|backend,node|false|
|Node Security|backend,node|false|
|React Hooks|frontend|false|

Matching posts:

```
3 posts
```

So:

```
total = 3
```

---

## Query 2 — Fetch Posts

Second query:

```javascript
Post.find(q)
  .sort({ createdAt: -1 })
  .skip(0)
  .limit(3)
  .populate("author", "name email")
```

Steps:

### 1. Filter posts

Find posts matching filter.

### 2. Sort

```
Newest posts first
```

### 3. Skip

```
skip 0 posts
```

### 4. Limit

```
return only 3 posts
```

### 5. Populate author

MongoDB replaces:

```
author: ObjectId
```

with actual user data.

Example:

```
author: {
  name: "Rahul",
  email: "rahul@mail.com"
}
```

---

# 8. Posts Returned From Database

Example result:

```json
[
  {
    "title": "Node Security",
    "tags": ["backend","node"],
    "author": {
      "name": "Rahul",
      "email": "rahul@mail.com"
    }
  },
  {
    "title": "Node Performance",
    "tags": ["backend","node"],
    "author": {
      "name": "Amit",
      "email": "amit@mail.com"
    }
  },
  {
    "title": "Node API Guide",
    "tags": ["backend","node"],
    "author": {
      "name": "Neha",
      "email": "neha@mail.com"
    }
  }
]
```

---

# 9. Metadata Creation

Controller calls:

```javascript
buildMeta(total, page, limit)
```

Example:

```
total = 3
page = 1
limit = 3
```

Metadata becomes:

```json
{
  "page": 1,
  "limit": 3,
  "totalItems": 3,
  "totalPages": 1
}
```

---

# 10. Final Response Sent to Client

```json
{
  "data": [
    {
      "title": "Node Security",
      "author": { "name": "Rahul", "email": "rahul@mail.com" }
    },
    {
      "title": "Node Performance",
      "author": { "name": "Amit", "email": "amit@mail.com" }
    },
    {
      "title": "Node API Guide",
      "author": { "name": "Neha", "email": "neha@mail.com" }
    }
  ],
  "meta": {
    "page": 1,
    "limit": 3,
    "totalItems": 3,
    "totalPages": 1
  }
}
```

---

# Complete Data Flow (Production Mental Model)

```
Frontend / Client
      │
      │ GET /api/posts?page=1&limit=3&q=node&tag=backend
      ▼
Express Router
      ▼
Controller (list)
      │
      │ Read query parameters
      │
      │ Build filter query
      │
      │ Run DB queries
      ▼
MongoDB
      │
      │ countDocuments()
      │ find()
      ▼
Controller builds metadata
      ▼
Response sent to client
```

---

💡 **Small improvement idea for your backend skills**

When you build APIs like this, try adding:

- caching (Redis)
    
- advanced filters
    
- sorting by likes/views
    
- cursor pagination (used by big systems)
    

These are the kinds of things that make a **backend developer stand out in startups**.

---

If you want, I can also show you something very interesting:

**How companies like Reddit, Twitter, and Medium design this same “list posts API” internally.**  
That architecture will level up your backend understanding a lot.