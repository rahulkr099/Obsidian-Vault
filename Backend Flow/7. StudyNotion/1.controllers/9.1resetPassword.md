## 🔹 RESET PASSWORD (Using Token)

### Function: `resetPassword(request, response)`

```
START resetPassword

TRY
    // Step 1: Read data from request body
    READ password
    READ confirmPassword
    READ token
```

---

### 🔸 Step 2: Validate Passwords Match

```
    IF password is not equal to confirmPassword
        RETURN response
            success = false
            message = "Passwords are not matching"
    END IF
```

📌 **Why this step?**  
Prevents accidental wrong password updates.

---

### 🔸 Step 3: Find User Using Token

```
    FETCH user from User collection
        WHERE token = provided token

    IF user does not exist
        RETURN response
            success = false
            message = "Token is invalid"
    END IF
```

📌 **Why this step?**  
Ensures token belongs to a valid user.

---

### 🔸 Step 4: Check Token Expiry

```
    IF resetPasswordExpires is less than current time
        RETURN response
            success = false
            message = "Token is expired, please regenerate token"
    END IF
```

📌 **Why this step?**  
Ensures token is still valid.

---

### 🔸 Step 5: Hash New Password

```
    HASH password using bcrypt
        SALT rounds = 10
```

📌 **Security best practice**  
Never store plain passwords.

---

### 🔸 Step 6: Update Password in Database

```
    UPDATE user record
        SET password = hashed password
```

💡 (Optional improvement)

```
    REMOVE token
    REMOVE resetPasswordExpires
```

---

### 🔸 Step 7: Send Success Response

```
    RETURN response
        success = true
        message = "Password reset successful"
```

---

### 🔸 Error Handling

```
CATCH error
    LOG error
    RETURN response
        success = false
        message = "Something went wrong while resetting password"
END TRY

END resetPassword
```

---

## 🧠 BIG-PICTURE FLOW (Easy to Explain)

```
User clicks "Forgot Password"
        ↓
Backend generates token
        ↓
Token stored with expiry
        ↓
Email sent with reset link
        ↓
User opens link
        ↓
User enters new password
        ↓
Token verified
        ↓
Password updated
```

---

## 🚀 NEXT-LEVEL IMPROVEMENTS (Forward Thinking)

1️⃣ **Clear token after reset**  
Avoid reuse of token.

2️⃣ **Password strength validation**

3️⃣ **Email confirmation after reset**

4️⃣ **Use HTTPS reset URL**

5️⃣ **Audit logs (security)**

---

## 🎯 Interview Answer Tip

If asked:

> “How do you implement forgot password?”

You can say:

- Generate secure token using crypto
    
- Store token with expiry
    
- Send reset link via email
    
- Verify token & expiry
    
- Hash new password and update
    

That’s **industry-standard** 👏

If you want next:

- 🧪 Test-case pseudocode
    
- 🔁 Service-layer refactor
    
- 🔐 Security hardening checklist
    

Just tell me 🚀