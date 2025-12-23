## 4. Create Notification API

```
WHEN POST /notify

  Validate request:
    - channel must be email or sms
    - recipient must exist

  IF idempotencyKey exists
    IF already seen
      RETURN existing notification

  Create notification record
    status = queued
    attempts = 0
    nextAttemptTime = now

  Save in notificationsMap
  Save idempotencyKey mapping

  Push id into queue

  Increment metrics.created

  RETURN notification id
```

👉 **Why idempotency matters:**  
Retrying the same request won’t send duplicate messages.
