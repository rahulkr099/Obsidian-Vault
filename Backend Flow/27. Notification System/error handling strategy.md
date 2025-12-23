## 13. Error Handling Strategy

```
IF bad request
  RETURN 400

IF duplicate idempotencyKey
  RETURN existing result

IF worker fails
  Retry with backoff

IF retries exhausted
  Mark as failed
```
