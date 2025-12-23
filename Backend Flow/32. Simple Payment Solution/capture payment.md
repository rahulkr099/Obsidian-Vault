## 📦 6. Capture Payment (Optional Flow)

```text
FUNCTION capturePayment(paymentId):

  FIND payment
  IF status NOT in (authorized, succeeded)
    RETURN error

  status = "captured"
  UPDATE timestamp

  SEND webhook "payment.captured"

  RETURN payment
```
