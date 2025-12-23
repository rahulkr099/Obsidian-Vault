## 📊 8. Job Lifecycle Flow

```text
Client
  ↓
POST /jobs
  ↓
Job stored in Redis queue
  ↓
Worker picks job
  ↓
Progress updates emitted
  ↓
Job completed OR retried on failure
```
