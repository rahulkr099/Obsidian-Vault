## ⏰ 6. Auto-Reset Counters (WOW – Cron Job)

```text
EVERY day at midnight:

  IF redisClient exists
    DELETE all Redis keys
  ELSE
    RESET in-memory counters
```
