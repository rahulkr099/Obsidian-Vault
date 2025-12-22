## 🔹 RESET PASSWORD TOKEN (Send Reset Link)

### Function: `resetPasswordToken(request, response)`

```
START resetPasswordToken

TRY
    // Step 1: Read email from request body
    READ email from request.body
```

---

### 🔸 Step 2: Validate Email (Check User Exists)

```
    FETCH user from User collection
        WHERE email = provided email

    IF user does not exist
        RETURN response
            success = false
            message = "Your email is not registered with us"
    END IF
```

📌 **Why this step?**  
Only registered users should be able to reset passwords.

---

### 🔸 Step 3: Generate Secure Reset Token

```
    GENERATE random token using crypto
        LENGTH = 20 bytes
        FORMAT = hexadecimal string
```

📌 **Why crypto?**  
Secure, unpredictable token for password reset.

---

### 🔸 Step 4: Save Token and Expiry Time in Database

```
    UPDATE user record
        SET token = generated token
        SET resetPasswordExpires = current time + 5 minutes
```

📌 **Why expiry?**  
Prevents misuse of old reset links.

---

### 🔸 Step 5: Create Reset Password URL

```
    CREATE reset URL
        FORMAT = "http://localhost:3000/update-password/{token}"
```

📌 **Frontend responsibility**  
This URL opens reset password page.

---

### 🔸 Step 6: Send Reset Email

```
    SEND email to user email
        SUBJECT = "Password Reset Link"
        BODY = reset URL
```

---

### 🔸 Step 7: Send Success Response

```
    RETURN response
        success = true
        message = "Email sent successfully, please check your email"
```

---

### 🔸 Error Handling

```
CATCH error
    LOG error
    RETURN response
        success = false
        message = "Something went wrong while sending reset mail"
END TRY

END resetPasswordToken
```

💡 **Improvement ideas**

- Use environment variable for frontend URL
    
- Add email template
    
- Rate limit reset requests
    
