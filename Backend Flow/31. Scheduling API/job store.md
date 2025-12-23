## 🗄️ 3. Job Store (In-Memory)

```text
STORE jobs = empty map

FUNCTION addJob(jobId, job):
  jobs[jobId] = job

FUNCTION getJob(jobId):
  RETURN jobs[jobId]

FUNCTION updateJob(jobId, updates):
  jobs[jobId] = merge(jobs[jobId], updates)
```
