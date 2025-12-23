## 🔍 6. API — Check Job Status

```text
API GET /status/:jobId

job = getJob(jobId)

IF job not found:
  RETURN 404

RETURN job
```
