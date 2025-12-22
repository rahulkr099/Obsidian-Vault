## 📌 1. `User.js` – User Authentication & Account
[[Auth.controller.js]]
[[ResetPassword.controller.js]]
[[Backend Flow/StudyNotion/auth.middleware.js|auth.middleware.js]]
```
START User Module

DEFINE User schema
    name
    email
    password
    role
    createdAt

FUNCTION registerUser(data)
    VALIDATE input
    CHECK if email already exists
    HASH password
    SAVE user in database
    RETURN success response
END

FUNCTION loginUser(credentials)
    FIND user by email
    COMPARE password
    IF valid
        GENERATE token
        RETURN token and user data
    ELSE
        RETURN error
END

FUNCTION getUserDetails(userId)
    FETCH user from database
    RETURN user data
END

END User Module
```
