## 🧮 4. Throttle Response

```text
IF allowed:
  RETURN 200 OK
ELSE:
  RETURN 429 Too Many Requests
  INCLUDE retryAfterMs
```
