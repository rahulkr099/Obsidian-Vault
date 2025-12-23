## ⏳ 1. DEBOUNCE — Schedule or Postpone Task

### API: `POST /debounce/:key`

```text
FUNCTION debounce(key, payload, windowMs):

  jobId = generateUUID()
  executeAt = currentTime() + windowMs

  STORE payload at "debounce:payload:jobId"
  SET TTL = windowMs * 5

  ADD jobId to ZSET "debounce:schedule:key" with score = executeAt

  RETURN "queued"
```

🧠 **What this does**  
If more requests come → new jobId is added with later timestamp.  
Worker will only execute jobs whose time has arrived.
