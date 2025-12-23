## 🛡️ 11. Cache Stampede Protection (Talk-Through)

```text
ON cache miss:

  ACQUIRE distributed lock (Redis)

  IF lock acquired
    FETCH from DB
    SET cache
    RELEASE lock
  ELSE
    WAIT and retry cache
```

_(You can say you’d use Redlock in production)_