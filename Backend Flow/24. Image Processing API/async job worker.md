## ⚙️ 6. Async Job Worker (Optional WOW)

```text
FUNCTION worker(job):

  UPDATE job status → processing

  TRY
    resultPath = applyOperations(job.imagePath, job.operations)
    UPDATE job status → done
    SAVE resultPath
  CATCH error
    UPDATE job status → failed
    SAVE error
```
