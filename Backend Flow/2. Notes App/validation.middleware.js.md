# 🧪 VALIDATION MIDDLEWARE — PSEUDOCODE

```
START validateNote

READ title and content from request

IF title OR content missing
    RETURN 400 error

CALL next middleware

END validateNote
```

💬

> “Validation prevents bad data early.”
