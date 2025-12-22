# 1️⃣2️⃣ Auth Middleware — `middlewares/auth.js`

### Purpose

Protects routes using JWT.

### Pseudocode

```
READ Authorization header

IF token missing
    RETURN unauthorized error

VERIFY token using secret
FETCH user from database

IF user not found
    RETURN unauthorized

ATTACH user to request
CALL next middleware
```

🗣

> “JWT authentication is stateless and scalable.”