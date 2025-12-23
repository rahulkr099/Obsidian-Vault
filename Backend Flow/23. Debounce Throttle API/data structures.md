## 🧾 Data Structures (Redis-backed)

### Debounce (Delayed Execution)

```text
Redis ZSET: debounce:schedule:<key>
  member = jobId
  score  = executeAtTimestamp

Redis STRING: debounce:payload:<jobId>
  value = latest payload (JSON)
```

---

### Throttle (Sliding Window)

```text
Redis ZSET: throttle:timestamps:<key>
  member = uniqueRequestId
  score  = requestTimestamp
```
