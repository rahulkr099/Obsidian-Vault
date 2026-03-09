This controller performs a **soft delete of a comment**.  
Soft delete means **the comment is not removed from the database**, it is only marked as deleted.

Let’s break it down clearly.

---

# 1. Pseudocode: Soft Delete Comment

```text
FUNCTION softDeleteComment(request, response, next)

    TRY

        // Step 1: Get comment ID from URL
        commentId = request.params.id


        // Step 2: Find comment in database
        comment = find comment in Comment collection using commentId


        // Step 3: Check if comment exists or already deleted
        IF comment does not exist OR comment.isDeleted is true THEN
            SEND response with status 404
            message = "Not found"
            RETURN
        ENDIF


        // Step 4: Check authorization
        IF comment.author is NOT equal to request.user._id THEN
            SEND response with status 403
            message = "Forbidden"
            RETURN
        ENDIF


        // Step 5: Perform soft delete
        comment.isDeleted = true


        // Step 6: Save updated comment
        save comment in database


        // Step 7: Send success response
        SEND response with status 204 (no content)


    CATCH error
        PASS error to next middleware

END FUNCTION
```

---

# 2. Practical Example: Data Flow

Imagine a **blog post page** where users can delete their own comments.

---

# Step 1: Client Sends Request

User clicks **Delete Comment**.

Request sent:

```http
DELETE /api/comments/C001
Authorization: Bearer token123
```

Express receives:

```javascript
req.params = {
  id: "C001"
}

req.user = {
  _id: "user789"
}
```

---

# Step 2: Request Reaches Controller

Route example:

```javascript
router.delete("/comments/:id", authMiddleware, commentController.softDelete);
```

Flow:

```text
Client
  ↓
Express Router
  ↓
Auth Middleware
(adds req.user)
  ↓
Controller (softDelete)
```

---

# Step 3: Controller Fetches Comment

Controller runs:

```javascript
Comment.findById("C001")
```

Database **comments collection**:

|_id|post|author|content|isDeleted|
|---|---|---|---|---|
|C001|65abc123|user789|Great article|false|
|C002|65abc123|user456|Nice explanation|false|

MongoDB returns:

```json
{
  "_id": "C001",
  "author": "user789",
  "content": "Great article",
  "isDeleted": false
}
```

---

# Step 4: Check If Comment Exists

Controller checks:

```text
comment exists?
comment.isDeleted == false?
```

If comment was already deleted:

```json
{
  "message": "Not found"
}
```

Status:

```text
404 Not Found
```

---

# Step 5: Authorization Check

Controller verifies ownership.

Example:

```text
comment.author = user789
req.user._id  = user789
```

So the user **is allowed**.

If another user tried to delete:

```text
comment.author = user789
req.user._id  = user111
```

Response:

```json
{
  "message": "Forbidden"
}
```

Status:

```text
403 Forbidden
```

---

# Step 6: Apply Soft Delete

Controller runs:

```javascript
comment.isDeleted = true
await comment.save()
```

Database updates row.

Before:

|_id|content|isDeleted|
|---|---|---|
|C001|Great article|false|

After:

|_id|content|isDeleted|
|---|---|---|
|C001|Great article|true|

The comment **still exists in database**, but now it's marked deleted.

---

# Step 7: Response Sent

Controller sends:

```text
204 No Content
```

Meaning:

```text
Request successful
but nothing returned
```

---

# Complete Data Flow

```text
Frontend
   │
   │ DELETE /api/comments/C001
   ▼
Express Router
   ▼
Auth Middleware
(adds req.user)
   ▼
Controller (softDelete)
   │
   │ Find comment
   ▼
MongoDB → comments collection
   │
   │ Check author permission
   │
   │ Set isDeleted = true
   ▼
MongoDB save()
   ▼
Controller sends 204 response
   ▼
Frontend removes comment from UI
```

---

# Why Soft Delete Is Used in Real Systems

Instead of deleting permanently, systems keep records for:

```text
Data recovery
Audit logs
Moderation review
Analytics
```

Example:

```text
Reddit
Facebook
YouTube
```

They **rarely hard delete immediately**.

---

💡 **Nice improvement idea for your backend**

When returning comments, always filter like this:

```javascript
Comment.find({ post: postId, isDeleted: false })
```

So deleted comments **never appear in the UI**, but still remain in the database for safety and auditing.