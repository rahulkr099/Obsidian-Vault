## 🔹 VERIFY PAYMENT (Signature Verification)

### Function: `verifyPayment(request, response)`

```
START verifyPayment

    READ razorpay_order_id from request body
    READ razorpay_payment_id from request body
    READ razorpay_signature from request body
    READ courses array from request body
    READ userId from request.user.id
```

---

### 🔸 Step 1: Validate Payment Fields

```
    IF any required payment field is missing
        RETURN response
            success = false
            message = "Payment Failed"
    END IF
```

---

### 🔸 Step 2: Generate Expected Signature

```
    CREATE bodyString = razorpay_order_id + "|" + razorpay_payment_id

    GENERATE expectedSignature using:
        HMAC SHA256
        secret = Razorpay secret key
```

---

### 🔸 Step 3: Compare Signatures

```
    IF expectedSignature matches razorpay_signature
        CALL enrollStudents(courses, userId)
        RETURN response
            success = true
            message = "Payment Verified"
    ELSE
        RETURN response
            success = false
            message = "Payment Failed"
    END IF
```

📌 **Why this step?**

- Ensures payment is genuine
    
- Prevents fake payment requests
    