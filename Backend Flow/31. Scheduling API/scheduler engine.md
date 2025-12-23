## ⏱️ 4. Scheduler Engine (Core Logic)

```text
FUNCTION scheduleTask(task, delaySeconds, executeCallback):

  jobId = generateUUID()

  job = {
    id: jobId,
    task: task,
    delaySeconds: delaySeconds,
    status: "scheduled",
    scheduledAt: currentTime(),
    executeAt: currentTime() + delaySeconds
  }

  addJob(jobId, job)

  SET TIMER after delaySeconds:
    updateJob(jobId, { status: "running" })

    TRY:
      executeCallback(job)
      updateJob(jobId, {
        status: "completed",
        completedAt: currentTime()
      })
    CATCH error:
      updateJob(jobId, {
        status: "failed",
        error: error.message
      })

  RETURN jobId
```
