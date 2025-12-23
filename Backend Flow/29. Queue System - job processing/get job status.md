## 🔍 4. Get Job Status

```text
FUNCTION getJobStatus(jobId):

  job = queue.GET_JOB(jobId)

  IF job does not exist
    RETURN "Job not found"

  state = job.GET_STATE()

  RETURN {
    jobId,
    type,
    state,
    progress,
    attemptsMade
  }
```
