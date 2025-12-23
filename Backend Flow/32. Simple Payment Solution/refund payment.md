## 🔄 7. Refund Payment

```text
FUNCTION refundPayment(paymentId, amount):

  FIND payment
  IF status NOT in (succeeded, captured)
    RETURN error

  CREATE refund object
  ADD refund to payment.refunds

  UPDATE payment timestamp

  SEND webhook "payment.refunded"

  RETURN refund
```
