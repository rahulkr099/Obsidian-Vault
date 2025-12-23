## 🔁 9. Idempotency (WOW Feature)

```text
FUNCTION transferMoney(request):

  IF request.idempotencyKey already processed
    RETURN previous result

  ELSE
    PROCESS transfer
    SAVE idempotencyKey with result
```

Prevents duplicate transfers on retry.
