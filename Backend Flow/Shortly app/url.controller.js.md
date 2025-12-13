Got it 👍  
Here is **ONE clean pseudocode snippet**, same compact style as before.  
No explanations. No extra text.

---

### 🔹 `url.controller.js` — PSEUDOCODE

```text
IMPORT URL database model
IMPORT unique ID generator
IMPORT environment variables
IMPORT user agent parser

DEFINE handleUserAnalytics
    READ user ID from authenticated request
    FIND all URLs for user
    IF no URLs found
        RETURN not found response
    END
    RETURN user analytics data
END

DEFINE handleShortenURL
    READ URL, custom ID, expiry from request body
    READ user ID from authenticated request

    IF URL missing
        RETURN error response
    END

    VALIDATE URL format
    IF invalid
        RETURN error response
    END

    IF URL already exists in database
        RETURN existing short URL
    END

    GENERATE nano ID (custom or auto)
    IF custom ID provided AND already exists
        RETURN error response
    END

    CREATE new short URL entry in database
    RETURN generated short URL
END

DEFINE handleGetAnalytics
    READ nano ID from request params
    IF nano ID missing
        RETURN error response
    END

    FIND URL entry by nano ID
    IF not found
        RETURN error response
    END

    RETURN URL analytics data
END

DEFINE handleRedirect
    READ nano ID from request params
    IF nano ID missing
        RETURN error response
    END

    FIND URL entry by nano ID
    IF not found
        RETURN error response
    END

    IF URL expired
        RETURN expired response
    END

    READ referrer, device, browser, IP
    ADD visit record to history
    INCREMENT click count
    UPDATE last visited time
    SAVE URL entry

    REDIRECT to original URL
END
```

---

This is **exactly revision-friendly, exam-friendly, and interview-friendly**.

If you want next:

- same style for **QR code service**
    
- **ultra-short version** (5–6 lines)
    
- **full backend pseudocode list** (index → routes → controllers → models)
    

Just say 👍