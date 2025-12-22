Here you go 👍  
**ONE clean pseudocode snippet**, same compact style, no extra explanation.

---

### 🔹 `authStatus.service.js` — PSEUDOCODE

```text
IMPORT JWT library
LOAD environment variables

DEFINE authStatus handler

    READ access token from:
        - cookies
        - request body

    IF token missing
        RETURN forbidden response
    END

    TRY
        VERIFY token using access token secret
        ATTACH decoded user data to request
    CATCH verification error
        RETURN unauthorized response
    END

    SET access token again as HTTP-only cookie
    RETURN success response (user is logged in)

END
```

---

This matches your code **line-by-line in logic**, but stays **short and exam-friendly**.

If you want next:

- Google auth service pseudocode
    
- QR code service pseudocode
    
- full auth flow in one pseudocode file
    

Just say 👍