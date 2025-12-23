## ⚙️ 5. Worker Logic (Background Processing)

```text
FUNCTION workerProcessor(job):

  steps = job.payload.steps OR 5

  FOR step FROM 1 TO steps:
    WAIT some time
    percent = (step / steps) * 100
    job.UPDATE_PROGRESS({ step, percent })

  IF job.payload.fail == true
    THROW error

  RETURN success result
```
