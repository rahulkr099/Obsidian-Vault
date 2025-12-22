### 🔹 `url.model.js` — PSEUDOCODE

```text
IMPORT database library
IMPORT unique ID generator

DEFINE URL schema

    STORE user reference ID (required)

    STORE short URL ID
        - must be unique
        - auto-generate if not provided

    STORE original redirect URL (required, unique)

    STORE expiration date (optional)

    STORE visit history as list
        FOR each visit:
            STORE timestamp
            STORE referrer
            STORE device
            STORE browser
            STORE IP address

    STORE total click count
    STORE last visited time

    ENABLE automatic createdAt and updatedAt timestamps

CREATE URL model from schema

EXPORT URL model
```

---

This pseudocode is **exam-ready, interview-ready, and revision-friendly**.

If you want next:

- controller pseudocode
    
- service layer pseudocode
    
- database flow pseudocode
    

Just say 👍
Nice 👍  
Here is **ONE clean pseudocode snippet**, exactly matching your style.