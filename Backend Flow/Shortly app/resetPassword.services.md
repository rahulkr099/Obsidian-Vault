Here you go 👍  
**ONE clean pseudocode snippet**, same compact style, no explanations.

---

### 🔹 `resetPassword.service.js` — PSEUDOCODE

```text
IMPORT User database model
IMPORT password hashing library
IMPORT crypto utility
IMPORT mail sender utility
LOAD environment variables

DEFINE resetPasswordToken handler
    READ email from request body
    IF email missing OR invalid format
        RETURN error response
    END

    FIND user by email
    IF user not found
        RETURN error response
    END

    GENERATE random reset token
    HASH reset token

    SAVE hashed token and expiry time in user record

    BUILD reset password URL with token and email
    SEND reset email to user

    RETURN success response
END


DEFINE resetPassword handler
    READ password, confirmPassword, email from request body

    IF password length invalid
        RETURN error response
    END

    IF password and confirmPassword do not match
        RETURN error response
    END

    READ reset token from request query
    IF token missing
        RETURN error response
    END

    HASH received token
    FIND user by email and hashed token
    IF user not found
        RETURN error response
    END

    IF token expired
        RETURN error response
    END

    HASH new password
    UPDATE user password
    CLEAR reset token and expiry fields

    RETURN success response
END
```

---

This is **short, clear, exam-ready, and revision-friendly**.

If you want:

- password reset flow diagram (text)
    
- ultra-short 5-line version
    
- combine all auth services into one pseudocode file
    

Just say 👍