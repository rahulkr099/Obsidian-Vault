## 5. Authentication Flow (JWT)

### Register User

```
WHEN POST /auth/register

  IF name OR email OR password missing
    RETURN error

  IF email already exists
    RETURN error

  Hash password

  Save new user

  Generate JWT token with userId

  RETURN token + user info
```

---

### Login User

```
WHEN POST /auth/login

  IF email OR password missing
    RETURN error

  Find user by email

  IF user not found OR password mismatch
    RETURN error

  Generate JWT token

  RETURN token + user info
```
