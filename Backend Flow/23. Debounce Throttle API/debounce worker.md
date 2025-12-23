## ⚙️ 2. DEBOUNCE WORKER — Execute Final Task

```text
WORKER LOOP (every 500ms):

  FOR each key matching "debounce:schedule:*":

    dueJobs = ZRANGEBYSCORE(key, -inf, now)

    FOR each jobId in dueJobs:
      REMOVE jobId from ZSET
      payload = GET "debounce:payload:jobId"
      EXECUTE payload
      DELETE "debounce:payload:jobId"
```

🧠 **Key Interview Point**

> “This works across multiple servers because Redis is shared.”