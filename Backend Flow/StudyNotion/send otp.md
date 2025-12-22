## 🔹 SEND OTP (Email Verification)

### Function: `sendOTP(request, response)`

```
START sendOTP

TRY
    READ email from request body

    IF email is missing
        RETURN response with error "Email is required"
    END IF

    SEARCH User collection for a user with this email

    IF user exists
        RETURN response
            success = false
            message = "User already registered"
    END IF

    GENERATE a 6-digit numeric OTP
        - no alphabets
        - no special characters

    CHECK OTP collection to see if same OTP already exists

    WHILE OTP already exists in database
        GENERATE a new 6-digit numeric OTP
    END WHILE

    CREATE otpPayload object
        otpPayload.email = email
        otpPayload.otp = generated OTP

    SAVE otpPayload in OTP collection

    RETURN response
        success = true
        message = "OTP sent successfully"
        otp (for testing / dev only)

CATCH any error
    LOG error
    RETURN response
        success = false
        message = error message
END TRY

END sendOTP
```

💡 **Improvement idea**

- Add OTP expiry (e.g., valid for 5 minutes)
    
- Limit OTP requests per email (anti-spam)
    
- Remove OTP from response in production
    
