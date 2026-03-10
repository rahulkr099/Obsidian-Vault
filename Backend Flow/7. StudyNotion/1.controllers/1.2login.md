## 🔹 LOGIN

### Function: `login(request, response)`

```
START login

TRY
    READ email and password from request body

    IF email or password is missing
        RETURN response
            success = false
            message = "All fields are required"
    END IF

    SEARCH User collection using email
        POPULATE additionalDetails (profile)

    IF user not found
        RETURN response
            success = false
            message = "User not registered"
    END IF

    COMPARE provided password with stored hashed password

    IF password matches
        CREATE JWT payload
            payload.email = user email
            payload.id = user id
            payload.accountType = user account type

        GENERATE JWT token with expiry = 2 hours

        ATTACH token to user object
        REMOVE password field from user object

        SET cookie options
            httpOnly = true
            expiry = 3 days

        SEND response with cookie
            success = true
            token
            user data
            message = "Logged in successfully"
    ELSE
        RETURN response
            success = false
            message = "Incorrect password"
    END IF

CATCH any error
    LOG error
    RETURN response
        success = false
        message = "Login failed. Try again"
END TRY

END login
```

💡 **Improvement ideas**

- Add refresh tokens
    
- Track login history
    
- Add account lock after multiple failed attempts
    

---
