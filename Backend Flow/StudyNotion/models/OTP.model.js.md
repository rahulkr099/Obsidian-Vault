## 📌 2. `OTP.js` – Email Verification

```
START OTP Module

DEFINE OTP schema
    email
    otp
    createdAt

FUNCTION generateOTP(email)
    CREATE random 6-digit OTP
    SAVE OTP with email
    SEND OTP via email
END

FUNCTION verifyOTP(email, enteredOTP)
    FETCH latest OTP for email
    IF OTP matches AND not expired
        RETURN success
    ELSE
        RETURN error
END

END OTP Module
```
