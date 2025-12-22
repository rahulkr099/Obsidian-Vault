## 🔹 SIGN UP (User Registration)

### Function: `signUp(request, response)`

```
START signUp

TRY
    READ following fields from request body
        firstName
        lastName
        email
        password
        confirmPassword
        accountType
        contactNumber
        otp

    IF any required field is missing
        RETURN response
            success = false
            message = "All fields are required"
    END IF

    IF password is not equal to confirmPassword
        RETURN response
            success = false
            message = "Password and confirm password do not match"
    END IF

    SEARCH User collection using email

    IF user already exists
        RETURN response
            success = false
            message = "User already registered"
    END IF

    FETCH most recent OTP for this email
        - sort by createdAt descending
        - limit result to 1

    IF no OTP found
        RETURN response
            success = false
            message = "OTP not found"
    END IF

    IF provided OTP does not match stored OTP
        RETURN response
            success = false
            message = "Invalid OTP"
    END IF

    HASH password using bcrypt with salt rounds = 10

    SET approved flag
        IF accountType is "Instructor"
            approved = false
        ELSE
            approved = true
        END IF

    CREATE Profile document with default null values
        gender = null
        dateOfBirth = null
        about = null
        contactNumber = null

    CREATE User document with
        firstName
        lastName
        email
        contactNumber
        hashed password
        accountType
        approved flag
        profile reference
        auto-generated avatar image URL

    SAVE user in database

    RETURN response
        success = true
        message = "User registered successfully"
        user details

CATCH any error
    LOG error
    RETURN response
        success = false
        message = "User cannot be registered. Try again later"
END TRY

END signUp
```

💡 **Improvement ideas**

- Delete OTP after successful signup
    
- Add email verification flag (`isVerified`)
    
- Enforce strong password rules
    
