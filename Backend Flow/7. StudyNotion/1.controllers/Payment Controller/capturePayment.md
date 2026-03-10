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
