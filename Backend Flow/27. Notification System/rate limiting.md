## 6. Rate Limiting (Per Channel)

```
BEFORE sending message

  Remove old timestamps (>1 second)

  IF sends in last second >= channel limit
    SKIP for now
    TRY in next worker tick
```

Example:

```
Email → 2 per second
SMS   → 5 per second
```
