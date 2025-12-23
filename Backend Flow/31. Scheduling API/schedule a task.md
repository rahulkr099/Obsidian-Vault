## 🌐 5. API — Schedule a Task

```text
API POST /schedule

INPUT:
  task
  delaySeconds

IF task missing OR delaySeconds missing:
  RETURN error

jobId = scheduleTask(task, delaySeconds, executeTask)

RETURN {
  jobId,
  message: "Task scheduled"
}
```
