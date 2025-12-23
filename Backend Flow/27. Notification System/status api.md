## 11. Status APIs

### Get Notification Status

```
WHEN GET /notifications/:id

  IF notification exists
    RETURN full record
  ELSE
    RETURN 404
```

### List Recent Notifications

```
WHEN GET /notifications

  RETURN last N notifications sorted by time
```
