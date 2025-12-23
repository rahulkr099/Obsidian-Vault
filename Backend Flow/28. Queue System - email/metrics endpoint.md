## 📊 6. Metrics Endpoint

```text
FUNCTION getMetrics():

  queue = initQueue()

  counts = queue.getJobCounts()
    (waiting, active, completed, failed)

  RETURN counts
```
