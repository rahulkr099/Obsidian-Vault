## ➕ 3. Add Job (Producer API)

```text
FUNCTION createJob(request):

  READ type, payload, priority, delayMs FROM request.body

  IF type is missing
    SET type = "default"

  MAP priority string to number
    high → 1
    normal → 5
    low → 10

  jobOptions:
    attempts = 3
    backoff = exponential (500ms)
    priority = mapped value
    delay = delayMs
    auto-remove completed jobs
    auto-remove failed jobs later

  jobData:
    id = generate UUID
    type = type
    payload = payload

  job = queue.ADD(type, jobData, jobOptions)

  RETURN job.id
```
