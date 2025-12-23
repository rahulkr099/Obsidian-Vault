## 6. Auth Middleware

```
FOR every protected route

  Read Authorization header

  IF token missing
    RETURN 401

  Verify JWT token

  IF invalid
    RETURN 401

  Attach userId to request

  CONTINUE to route
```
