## 🚦 3. THROTTLE — Sliding Window Rate Limit

### API: `POST /throttle/:key`

```text
FUNCTION throttle(key, limit, windowMs):

  zkey = "throttle:timestamps:key"
  now = currentTime()
  windowStart = now - windowMs

  REMOVE from zkey all entries with score < windowStart
  ADD (now, uniqueRequestId) to zkey
  count = ZCARD(zkey)

  IF count <= limit:
    ALLOW request
  ELSE:
    earliest = ZRANGE(zkey, 0, 0)
    retryAfter = (earliest.score + windowMs) - now
    BLOCK request with retryAfter
```

🧠 **Why Sliding Window is Better**

```text
Fixed window → burst allowed at boundary
Sliding window → fair & smooth
```
