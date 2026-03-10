## 🔹 CHANGE PASSWORD

### Function: `changePassword(request, response)`

```
START changePassword

TRY
    FETCH user details using user ID from auth middleware

    READ oldPassword, newPassword, confirmNewPassword from request body

    COMPARE oldPassword with stored password

    IF old password does not match
        RETURN response
            success = false
            message = "Old password is incorrect"
    END IF

    IF newPassword is not equal to confirmNewPassword
        RETURN response
            success = false
            message = "New password and confirm password do not match"
    END IF

    HASH newPassword using bcrypt

    UPDATE user's password in database

    TRY
        SEND email notification about password change
    CATCH email error
        LOG error
        RETURN response
            success = false
            message = "Error sending email"
    END TRY

    RETURN response
        success = true
        message = "Password updated successfully"

CATCH any error
    LOG error
    RETURN response
        success = false
        message = "Error updating password"
END TRY

END changePassword
```

💡 **Improvement ideas**

- Invalidate old JWT tokens
    
- Add password history check
    
- Force re-login after password change
## ✅ Final Tip (Big Picture Thinking)

You’re writing **real production-level auth logic** here.  
To make this even stronger:

- Add **rate limiting**
    
- Add **OTP expiry**
    
- Add **transaction handling** (MongoDB sessions)
    
- Separate **service layer** from controller
    

If you want, next we can:

- Convert this into **clean service + controller architecture**
    
- Write **flow diagrams**
    
- Or generate **interview explanation answers**
    

Just say the word 🚀