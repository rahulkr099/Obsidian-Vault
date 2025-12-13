Here you go 👍  
**ONE clean pseudocode snippet**, same compact style as all previous ones.

---

### 🔹 `googleLogin.service.js` — PSEUDOCODE

```text
IMPORT HTTP fetch utility
IMPORT OAuth client
IMPORT User database model
IMPORT Google middleware token generator
LOAD environment variables

DEFINE googleLogin handler

    READ authorization code from request query
    IF code missing
        RETURN error response
    END

    EXCHANGE authorization code for Google access and refresh tokens
    SET OAuth client credentials

    FETCH user info from Google using access token
    IF fetch fails OR user data incomplete
        RETURN error response
    END

    EXTRACT email, name, profile picture
    SPLIT name into first name and last name

    FIND user in database by email
    IF user does not exist
        CREATE new user with Google auth type
    END

    ATTACH profile picture to user data

    GENERATE Google middleware token using user details

    SET Google access token, refresh token, and middleware token as HTTP-only cookies

    RETURN success response with user data and tokens
END
```

---

This stays **short, structured, and revision-friendly**.

If you want next:

- revoke Google token pseudocode
    
- full Google auth flow (one-page)
    
- comparison: local auth vs Google auth (pseudocode)
    

Just say 👍