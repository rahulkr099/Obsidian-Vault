Understood 👍  
Here is **ONE clean pseudocode snippet**, same compact style as before.  
No notes. No explanation. Just **pure pseudocode**.

---

### 🔹 `user.controller.js` — PSEUDOCODE

```text
IMPORT password hashing library
IMPORT user database model
IMPORT access & refresh token generators
IMPORT JWT library
LOAD environment variables

DEFINE signup handler
    READ user details from request body
    IF any required field missing
        RETURN error response
    END

    IF user already exists in database
        RETURN error response
    END

    HASH password
    CREATE new user in database
    RETURN success response
END

DEFINE login handler
    READ email and password from request body
    IF email or password missing
        RETURN error response
    END

    FIND user by email
    IF user not found
        RETURN error response
    END

    COMPARE input password with stored password
    IF password invalid
        RETURN error response
    END

    GENERATE access token
    GENERATE refresh token
    SAVE refresh token in database

    REMOVE sensitive fields from user data
    SET access token and refresh token as HTTP-only cookies
    RETURN success response with user data
END

DEFINE logout handler
    CLEAR access token cookie
    CLEAR refresh token cookie
    RETURN logout success response
END

DEFINE refresh access token handler
    READ refresh token from cookies, body, or headers
    IF refresh token missing
        RETURN unauthorized response
    END

    VERIFY refresh token using JWT
    IF token invalid or expired
        RETURN unauthorized response
    END

    FIND user using token data
    IF user not found OR token does not match database
        RETURN unauthorized response
    END

    GENERATE new access token
    GENERATE new refresh token
    UPDATE refresh token in database

    SET new tokens as HTTP-only cookies
    RETURN success response with new tokens
END
```

---

This is **exam-ready, interview-ready, and revision-friendly**.

If you want next:

- controller pseudocode split per function
    
- ultra-short 10-line version
    
- same style for URL controllers
    

Just say 👍