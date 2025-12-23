## 5. Worker Loop (Runs Every Second)

```
EVERY worker interval

  Remove delivered notifications from queue

  Find notifications eligible to send:
    - status not delivered
    - nextAttemptTime <= now

  Group eligible notifications by channel

  FOR each channel
    Process in batches
```
