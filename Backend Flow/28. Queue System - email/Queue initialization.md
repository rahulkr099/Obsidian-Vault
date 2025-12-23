## 📦 2. Queue Initialization (Redis + Bull)

```text
GLOBAL emailQueue
GLOBAL redisClient

FUNCTION initQueue():

  IF emailQueue already exists
    RETURN emailQueue

  redisClient = CONNECT Redis using REDIS_URL

  emailQueue = CREATE Bull Queue "email-queue"
    USING redisClient for commands
    USING separate redis connections for pub/sub

  ON queue error:
    LOG error

  ON job completed:
    LOG jobId + success

  ON job failed:
    LOG jobId + reason

  RETURN emailQueue
```
