## 📩 3. Enqueue Email API

```text
FUNCTION enqueueEmail(request):

  READ to, subject, text, html, idempotencyKey FROM request.body

  IF to OR subject OR (text AND html missing)
    RETURN 400 Bad Request

  ------------------------------------------------
  // IDEMPOTENCY
  ------------------------------------------------
  IF idempotencyKey exists
    jobId = "email:" + idempotencyKey
  ELSE
    jobId = HASH(to + subject + text + html)

  queue = initQueue()

  TRY
    ADD job to queue:
      name = "send-email"
      data = { to, subject, text, html }
      options:
        jobId = jobId
        attempts = 5
        backoff = exponential (1s, 2s, 4s…)
        auto-remove completed jobs
        keep failed jobs for debugging

    RETURN 202 Accepted (queued)
  
  CATCH duplicate jobId error
    RETURN 200 Already queued
```
