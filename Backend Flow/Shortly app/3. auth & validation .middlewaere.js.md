Understood Rahul 👍  
Here is **ONE clean pseudocode snippet**, same style as your code, **no extra notes**.

---

### 🔹 `auth.middleware.js` — PSEUDOCODE

```text
IMPORT JWT library
LOAD environment variables

DEFINE auth middleware (request, response, next)

TRY
    SET token from:
        - cookies accessToken
        - request body accessToken
        - Authorization header (Bearer token)

    IF token not found
        SET googleToken from cookies

        IF googleToken also not found
            RETURN 401 (Token missing)
        END
    END

    TRY
        IF normal token exists
            VERIFY token using ACCESS_TOKEN_SECRET
        ELSE
            VERIFY googleToken using GOOGLE_TOKEN_SECRET
        END

        IF decoded data invalid
            RETURN 401 (Invalid or expired token)
        END

        ATTACH decoded user data to request
    CATCH token verification error
        RETURN 401 (Token invalid)
    END

    CALL next middleware
CATCH unexpected error
    RETURN 500 (Internal server error)
END
```

---

This is **perfectly exam-ready and interview-ready**.

If you want:

- ultra-short version
    
- flow diagram in text
    
- same pseudocode for controllers
    

Just say 👍