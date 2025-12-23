## 8. Retry with Exponential Backoff ⭐

```
ON failure

  attempts += 1
  metrics.retries += 1

  IF attempts >= MAX_RETRIES
    status = failed
    metrics.failed += 1
    STOP

  ELSE
    backoffTime = baseDelay * (2 ^ (attempts - 1))
    add small random jitter

    nextAttemptTime = now + backoffTime
    status = scheduled
```

👉 **Why this is good:**  
Avoids hammering external providers when they are unstable.
