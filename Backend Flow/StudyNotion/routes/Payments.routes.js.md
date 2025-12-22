## 📌 4. `Payments.js` – Payment Processing

```
START Payments Module

DEFINE Payment schema
    userId
    courseId
    amount
    status
    paymentDate

FUNCTION initiatePayment(userId, courseId)
    CALCULATE amount
    CREATE payment order
    RETURN payment gateway data
END

FUNCTION verifyPayment(paymentResponse)
    VALIDATE payment with gateway
    IF success
        UPDATE payment status
        ENROLL user in course
    ELSE
        MARK payment as failed
    ENDIF
END

END Payments Module
```
