# 1️⃣7️⃣ Post Controller — `controllers/postController.js`

### Create

```
VALIDATE request
CREATE post with author
RETURN post
```

### List

```
APPLY filters
APPLY pagination
FETCH posts
RETURN data + metadata
```

### Get

```
FETCH post
FETCH recent comments
RETURN combined response
```

### Update

```
CHECK ownership
UPDATE fields
SAVE post
```

### Soft Delete

```
CHECK ownership
MARK post deleted
```

### Like

```
INCREMENT likes atomically
RETURN new count
```

### Analytics

```
GROUP posts by author
COUNT posts and likes
RETURN top authors
```

🗣

> “Aggregation pipelines show database-side computation.”