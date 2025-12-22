# 9️⃣ `Post Model` — `models/Post.js`

### Purpose

Represents blog posts.

### Pseudocode

```
DEFINE Post schema:
    title (required, searchable)
    content (required, searchable)
    author (reference to User)
    tags (list of strings)
    likes (number)
    isDeleted (boolean)

ENABLE timestamps
ENABLE versioning

CREATE indexes for:
    text search
    tag + date sorting

EXPORT Post model
```

🗣

> “Soft delete protects data and supports recovery.”