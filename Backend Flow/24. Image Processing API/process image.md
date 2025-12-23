## 🛠️ 4. Process Image (Core Logic)

```text
FUNCTION processImage(request):

  READ imageId and operations list

  IF image does not exist
    RETURN error

  IF operations are small (resize, format, compress)
    CALL processSynchronously()
    RETURN result URL
  ELSE
    ENQUEUE job to background queue
    RETURN jobId
```
