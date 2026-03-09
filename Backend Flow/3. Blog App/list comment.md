This controller **returns all comments for a specific post**.  
Let’s understand it clearly with **pseudocode** and a **real practical data flow example**.

---

# 1. Pseudocode: List Comments for a Post

```text
FUNCTION listCommentsForPost(request, response, next)

    TRY

        // Step 1: Get post ID from URL
        postId = request.params.postId


        // Step 2: Fetch comments from database
        comments = find comments in Comment collection
                   where
                        post = postId
                        isDeleted = false


        // Step 3: Sort comments
        order comments by createdAt in descending order
        (newest comments first)


        // Step 4: Include author information
        populate author field with name


        // Step 5: Send comments as response
        SEND response with comments list


    CATCH error
        PASS error to next middleware

END FUNCTION
```

---

# 2. Practical Example: Data Flow

Imagine a **blog post page** where users read comments.

---

# Step 1: Client Sends Request

Frontend loads comments for a post.

Request:

```http
GET /api/posts/65abc123/comments
```

Express receives:

```javascript
req.params = {
  postId: "65abc123"
}
```

---

# Step 2: Request Reaches Controller

Example route:

```javascript
router.get("/posts/:postId/comments", commentController.listForPost);
```

Flow:

```text
Client
   ↓
Express Router
   ↓
Controller (listForPost)
```

---

# Step 3: Controller Queries Database

Controller runs:

```javascript
Comment.find({
  post: "65abc123",
  isDeleted: false
})
```

Database **comments collection**:

|_id|post|author|content|createdAt|isDeleted|
|---|---|---|---|---|---|
|C001|65abc123|U1|Great article|10:00|false|
|C002|65abc123|U2|Very helpful|10:05|false|
|C003|65abc123|U3|Nice explanation|10:07|false|
|C004|65abc123|U4|Spam comment|10:08|true|

MongoDB filters:

```text
post = 65abc123
isDeleted = false
```

Remaining comments:

|_id|author|content|
|---|---|---|
|C001|U1|Great article|
|C002|U2|Very helpful|
|C003|U3|Nice explanation|

Deleted comment **C004 is removed**.

---

# Step 4: Sort Comments

Controller applies:

```javascript
.sort({ createdAt: -1 })
```

Meaning:

```text
Newest comment first
```

Sorted result:

|_id|content|time|
|---|---|---|
|C003|Nice explanation|10:07|
|C002|Very helpful|10:05|
|C001|Great article|10:00|

---

# Step 5: Populate Author

Each comment stores author ID.

Example:

```text
author = ObjectId("U1")
```

MongoDB fetches from **users collection**.

Users table:

|_id|name|
|---|---|
|U1|Rahul|
|U2|Amit|
|U3|Neha|

After populate:

```json
{
  "content": "Nice explanation",
  "author": {
    "name": "Neha"
  }
}
```

---

# Step 6: Controller Sends Response

Final response:

```json
[
  {
    "content": "Nice explanation",
    "author": { "name": "Neha" }
  },
  {
    "content": "Very helpful",
    "author": { "name": "Amit" }
  },
  {
    "content": "Great article",
    "author": { "name": "Rahul" }
  }
]
```

Frontend displays comments under the post.

---

# Complete Data Flow

```text
Frontend
   │
   │ GET /api/posts/65abc123/comments
   ▼
Express Router
   ▼
Controller (listForPost)
   │
   │ Query comments
   ▼
MongoDB → comments collection
   │
   │ Filter deleted comments
   │
   │ Sort by newest
   │
   │ Populate author name
   ▼
Controller sends response
   ▼
Frontend displays comments
```

---

# Backend Insight

This API demonstrates **three common backend practices**:

```text
Filtering (isDeleted = false)
Sorting (newest comments first)
Population (joining user data)
```

Almost every platform uses this pattern:

```text
YouTube → comments under video
Reddit → comments under post
Instagram → comments under photo
```

---

💡 **Good improvement idea for your project**

Add **pagination for comments**, because large posts can have thousands of comments.

Example request:

```text
GET /posts/:postId/comments?page=1&limit=10
```

This makes your API **scalable and production-ready**.