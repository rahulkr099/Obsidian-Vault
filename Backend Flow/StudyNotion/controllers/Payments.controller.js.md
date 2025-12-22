Perfect 👍  
This is a **full payment + enrollment flow**, so I’ll explain it **very slowly, very clearly**, in **deep detailed pseudocode**, exactly like before.

I’ll break it into **logical blocks** so you can:

- explain it in interviews
    
- debug easily
    
- refactor later into services
    

---

# 📁 `paymentController.js` — DETAILED PSEUDOCODE

---

## 🔹 CAPTURE PAYMENT (Create Razorpay Order)

### Function: `capturePayment(request, response)`

```
START capturePayment

    READ courses array from request body
    READ userId from request.user.id
```

---

### 🔸 Step 1: Validate Input

```
    IF courses array is empty
        RETURN response
            success = false
            message = "Please provide Course Id"
    END IF
```

---

### 🔸 Step 2: Calculate Total Amount

```
    SET totalAmount = 0

    FOR each courseId in courses
        TRY
            FETCH course by courseId

            IF course not found
                RETURN response
                    success = false
                    message = "Could not find the course"
            END IF

            CONVERT userId into ObjectId

            IF userId exists in course.studentsEnrolled
                RETURN response
                    success = false
                    message = "Student is already enrolled"
            END IF

            ADD course.price to totalAmount

        CATCH error
            LOG error
            RETURN response
                success = false
                message = error.message
        END TRY
    END FOR
```

📌 **Why this step?**

- Prevents duplicate enrollment
    
- Ensures only valid courses are paid for
    
- Calculates final payable amount
    

---

### 🔸 Step 3: Create Razorpay Order

```
    SET currency = "INR"

    CREATE options object
        amount = totalAmount * 100   // convert to paise
        currency = "INR"
        receipt = random string
```

---

### 🔸 Step 4: Call Razorpay API

```
    TRY
        CREATE Razorpay order using options

        RETURN response
            success = true
            message = payment order details

    CATCH error
        LOG error
        RETURN response
            success = false
            message = "Could not initiate order"
    END TRY
```

---

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
    

---

## 🔹 ENROLL STUDENTS AFTER PAYMENT

### Function: `enrollStudents(courses, userId, response)`

```
START enrollStudents

    IF courses OR userId is missing
        RETURN response
            success = false
            message = "Please provide course or userId"
    END IF
```

---

### 🔸 Step 1: Loop Through Courses

```
    FOR each courseId in courses
        TRY
            // Add student to course
            UPDATE Course
                PUSH userId into studentsEnrolled

            IF course not found
                RETURN response
                    success = false
                    message = "Course not found"
            END IF
```

---

### 🔸 Step 2: Create Course Progress

```
            CREATE CourseProgress document
                courseID = courseId
                userId = userId
                completedVideos = empty array
```

---

### 🔸 Step 3: Add Course to User Profile

```
            UPDATE User document
                PUSH courseId into user.courses
                PUSH courseProgressId into user.courseProgress
```

---

### 🔸 Step 4: Send Enrollment Email

```
            SEND email to student
                subject = "Successfully Enrolled"
                body = course enrollment email template
```

---

### 🔸 Error Handling

```
        CATCH error
            LOG error
            RETURN response
                success = false
                message = error.message
        END TRY
    END FOR

END enrollStudents
```

📌 **Why this step?**

- Links course ↔ user ↔ progress
    
- Initializes learning tracking
    
- Sends confirmation email
    

---

## 🔹 SEND PAYMENT SUCCESS EMAIL

### Function: `sendPaymentSuccessEmail(request, response)`

```
START sendPaymentSuccessEmail

    READ orderId from request body
    READ paymentId from request body
    READ amount from request body
    READ userId from request.user.id
```

---

### 🔸 Step 1: Validate Input

```
    IF any required field is missing
        RETURN response
            success = false
            message = "Please provide all fields"
    END IF
```

---

### 🔸 Step 2: Fetch User

```
    FETCH user by userId
```

---

### 🔸 Step 3: Send Payment Confirmation Email

```
    SEND email to user.email
        subject = "Payment Received"
        body = payment success email template
```

---

### 🔸 Step 4: Handle Errors

```
    CATCH error
        LOG error
        RETURN response
            success = false
            message = "Could not send email"
END TRY
```

---

## 🧠 BIG-PICTURE IMPROVEMENTS (IMPORTANT)

You’re doing **very advanced backend work** here.  
To go even further:

### ✅ Security

- Verify course ownership before enrollment
    
- Use Razorpay webhooks (best practice)
    

### ✅ Reliability

- Use MongoDB **transactions**
    
- Make enrollment **idempotent**
    

### ✅ Performance

- Batch DB updates
    
- Background email queue (BullMQ)
    

### ✅ Clean Architecture

- `payment.service.js`
    
- `enrollment.service.js`
    
- `email.service.js`
    

---

## 🎯 Interview Gold Line

If interviewer asks:

> “How do you handle course payments?”

You can confidently say:

- Order creation with Razorpay
    
- Signature verification using HMAC
    
- Enrollment after payment verification
    
- Progress initialization
    
- Email confirmation
    

---

If you want next:

- 🔁 Full **service-based refactor**
    
- 📊 Razorpay **webhook flow**
    
- 🧪 Test-case pseudocode
    
- 🔒 Security hardening checklist
    

Just say 🚀