## 🧾 4. Create Payment Intent

```text
FUNCTION createPayment(request):

  IF idempotencyKey exists AND already processed
    RETURN stored response

  VALIDATE amount

  CREATE payment with:
    status = "requires_payment_method"
    id = generate unique id

  SAVE payment in store

  GENERATE paymentUrl

  IF simulate == "auto"
    RANDOMLY mark payment as succeeded OR failed
    SEND webhook event

  STORE response against idempotencyKey (if present)

  RETURN payment + paymentUrl
```
