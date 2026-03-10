## 📌 1. `User.js` – User Account

```
START User Module

DEFINE User schema
    firstName
    lastName
    email
    password
    role (student / instructor / admin)
    coursesEnrolled
    createdAt

FUNCTION registerUser(data)
    VALIDATE input
    CHECK if user already exists
    HASH password
    SAVE user
    SEND OTP
END

FUNCTION loginUser(credentials)
    FIND user by email
    VERIFY password
    GENERATE auth token
    RETURN token
END

END User Module
```
