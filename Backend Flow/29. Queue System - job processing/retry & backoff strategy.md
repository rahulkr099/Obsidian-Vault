## 🔁 9. Retry & Backoff Strategy

```text
IF job fails:
  IF attempts remaining
    WAIT backoff delay
    RETRY job
  ELSE
    MOVE job to failed state
```
