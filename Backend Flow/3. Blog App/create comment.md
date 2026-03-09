This controller creates a **comment on a post**. Let’s understand it in two parts:

1️⃣ **Pseudocode (logic without syntax)**  
2️⃣ **Practical example showing how data flows step-by-step**

---

# 1. Pseudocode: Create Comment

```text
FUNCTION createComment(request, response, next)

    TRY

        // Step 1: Prepare data for validation
        bodyData = merge request.body with:
                   postId = request.body.postId OR request.body.post


        // Step 2: Validate comment input
        validationResult = validate bodyData using schema

        IF validationResult contains error THEN
            SEND response with status 400
            message = validationResult.error.message
            RETURN
        ENDIF


        // Step 3: Check if the post exists
        post = find post in Post collection using validationResult.postId

        IF post does not exist OR post.isDeleted is true THEN
            SEND response with status 404
            message = "Post not found"
            RETURN
        ENDIF


        // Step 4: Create comment
        comment = create new document in Comment collection with
                  post = post._id
                  author = request.user._id
                  content = validationResult.content


        // Step 5: Send response
        SEND response with status 201 and created comment


    CATCH error
        PASS error to next middleware

END FUNCTION
```

---

# 2. Practical Example: How Data Flows

Imagine a **blog post page** where users can comment.

---

# Step 1: Client Sends Request

User writes a comment on the frontend.

Request:

```http
POST /api/comments
Authorization: Bearer token123
Content-Type: application/json
```

Request body:

```json
{
  "postId": "65abc123",
  "content": "This article helped me understand Node.js!"
}
```

Express receives:

```javascript
req.body = {
  postId: "65abc123",
  content: "This article helped me understand Node.js!"
}

req.user = {
  _id: "user789"
}
```

`req.user` was added by **authentication middleware**.

---

# Step 2: Controller Handles Flexible Input

Controller supports two possible inputs:

```json
{
  "postId": "65abc123"
}
```

OR

```json
{
  "post": "65abc123"
}
```

So controller converts both into:

```javascript
postId = req.body.postId || req.body.post
```

Final validation data:

```json
{
  "postId": "65abc123",
  "content": "This article helped me understand Node.js!"
}
```

---

# Step 3: Validate Input

Schema checks:

```text
postId → required
content → required string
```

If invalid request:

```json
{
  "content": ""
}
```

Response:

```json
{
  "message": "content is required"
}
```

Status:

```text
400 Bad Request
```

---

# Step 4: Check if Post Exists

Controller runs:

```javascript
Post.findById("65abc123")
```

Database **posts collection**:

|_id|title|isDeleted|
|---|---|---|
|65abc123|Learning Node.js|false|
|77xyz111|React Basics|false|

MongoDB finds:

```json
{
  "_id": "65abc123",
  "title": "Learning Node.js",
  "isDeleted": false
}
```

If post didn’t exist:

```json
{
  "message": "Post not found"
}
```

Status:

```text
404 Not Found
```

---

# Step 5: Create Comment

Controller runs:

```javascript
Comment.create({
  post: post._id,
  author: req.user._id,
  content: value.content
})
```

Example values:

```text
post   = 65abc123
author = user789
content = "This article helped me understand Node.js!"
```

MongoDB inserts into **comments collection**:

|_id|post|author|content|
|---|---|---|---|
|C001|65abc123|user789|This article helped me understand Node.js!|

---

# Step 6: Response Sent to Client

Controller sends:

```json
{
  "_id": "C001",
  "post": "65abc123",
  "author": "user789",
  "content": "This article helped me understand Node.js!"
}
```

Status:

```text
201 Created
```

Frontend immediately displays the **new comment**.

---

# Complete Data Flow

```text
Frontend
   │
   │ POST /api/comments
   ▼
Express Router
   ▼
Auth Middleware
(adds req.user)
   ▼
Controller (create comment)
   │
   │ Validate request body
   │
   │ Check if post exists
   ▼
MongoDB → posts collection
   │
   │ Create comment
   ▼
MongoDB → comments collection
   ▼
Controller sends response
   ▼
Frontend displays comment
```

---

# Real Backend Insight

This controller demonstrates **three important backend concepts**:

```text
1. Input validation
2. Resource verification (post exists)
3. Relationship creation (comment → post)
```

This pattern appears in almost every system:

```text
Instagram → comment on photo
YouTube → comment on video
Reddit → comment on post
```

---

💡 **Interesting improvement idea**

Professional systems also store:

```text
comment count on posts
```

When a comment is created:

```text
Post.commentsCount += 1
```

This prevents running expensive queries every time a post loads and makes the system **much faster at scale**.