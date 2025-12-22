# 8️⃣ `User Model` — `models/User.js`

### Purpose

Stores user credentials securely.

### Pseudocode

```
DEFINE User schema:
    name (required)
    email (unique, indexed)
    password (hashed)

ENABLE timestamps

BEFORE saving user:
    IF password changed
        HASH password

DEFINE method to compare passwords

EXPORT User model
```

🗣

> “Passwords are never stored in plain text.”