# 1️⃣5️⃣ Auth Controller — `controllers/authController.js`

### Purpose

Handles user signup and login.

### Register

```
VALIDATE input
CHECK if email exists
CREATE user
GENERATE JWT
RETURN user + token
```

### Login

```
VALIDATE input
FETCH user by email
COMPARE passwords
GENERATE JWT
RETURN user + token
```

🗣

> “Auth logic stays inside controller, not routes.”