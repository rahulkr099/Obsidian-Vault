Got it 👍  
Here is **ONE clean pseudocode snippet**, same compact style, no explanations.

---

### 🔹 `googleAuth.services.js` — PSEUDOCODE

```text
IMPORT OAuth client
IMPORT User database model
IMPORT Google middleware token generator

DEFINE checkGoogleAccessToken handler
    READ Google access token from cookies or request body

    IF access token missing
        RETURN unauthorized response
    END

    FETCH user info from Google using access token
    IF fetch fails
        RETURN unauthorized response
    END

    FIND user in database using email from Google
    GENERATE Google middleware token for user

    SET Google access token and middleware token as HTTP-only cookies
    RETURN success response with user data
END

DEFINE authenticateGoogleRequest handler
    READ Google refresh token from cookies or request body

    IF refresh token missing
        RETURN unauthorized response
    END

    CALL refreshGoogleToken using refresh token
    RECEIVE new access token and refresh token

    SET new tokens as HTTP-only cookies
    RETURN success response with tokens
END

DEFINE refreshGoogleToken function
    SET OAuth client credentials using refresh token
    REQUEST new access token from Google
    RETURN new credentials
END
```

---

This is **short, revision-friendly, and exam-ready**.

If you want next:

- Google login (redirect) pseudocode
    
- revoke Google token pseudocode
    
- full Google auth flow in one snippet
    

Just say 👍