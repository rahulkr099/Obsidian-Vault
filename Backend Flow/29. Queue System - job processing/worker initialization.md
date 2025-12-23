## 🧵 6. Worker Initialization

```text
FUNCTION startWorker():

  worker = CREATE Worker(queueName, workerProcessor)
    concurrency = N
    redisConnection

  ON job completed:
    LOG success

  ON job failed:
    LOG error
```
