## 🧠 5. In-Memory Fallback (Single Process)

### Debounce (Memory)

```text
MAP debounceMap[key] = { timer, payload }

ON request:
  CLEAR existing timer
  SET new timer(windowMs)
  STORE payload

ON timer expiry:
  EXECUTE payload
  DELETE key
```

---

### Throttle (Memory)

```text
MAP throttleMap[key] = list of timestamps

ON request:
  REMOVE timestamps older than now - windowMs
  ADD now

  IF size <= limit:
    ALLOW
  ELSE:
    BLOCK
```
