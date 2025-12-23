## 🔄 4. Pub/Sub Invalidation (Multi-Instance Sync)

```text
SUBSCRIBE to "cache-invalidate" channel

ON message(id):
  key = cacheKey(id)
  LRU.DELETE(key)
```

_(Keeps in-memory caches in sync across servers)_
