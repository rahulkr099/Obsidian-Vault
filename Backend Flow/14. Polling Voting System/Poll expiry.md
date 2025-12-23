## ⏰ 6. Poll Expiry Cleaner (WOW – Cron Job)

```text
EVERY 10 minutes:

  FIND polls WHERE expiresAt < current time
  DELETE expired polls
```
