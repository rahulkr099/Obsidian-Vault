## 🔑 10. Idempotency Handling

```text
ON request with Idempotency-Key:

  IF key already exists
    RETURN saved response

  ELSE
    PROCESS request
    SAVE response against key
```
