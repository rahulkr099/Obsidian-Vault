## 📦 2. Queue Initialization

```text
GLOBAL redisConnection
GLOBAL queue
GLOBAL queueEvents

FUNCTION initQueue():

  IF queue already exists
    RETURN queue

  redisConnection = CONNECT Redis(host, port)

  queue = CREATE Queue(queueName, redisConnection)

  queueEvents = CREATE QueueEvents(queueName, redisConnection)

  RETURN queue
```
