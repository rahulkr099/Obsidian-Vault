## 💳 5. Simulate Client Payment

```text
FUNCTION pay(paymentId, outcome):

  FIND payment by paymentId
  IF not found
    RETURN error

  IF outcome == "succeed"
    status = "succeeded"
  ELSE IF outcome == "fail"
    status = "failed"
  ELSE
    status = "requires_payment_method"

  UPDATE payment timestamp

  SEND webhook event "payment.<status>"

  RETURN payment
```
