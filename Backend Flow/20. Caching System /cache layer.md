## 📦 3. Cache Layer (LRU + Redis)

### Get from Cache

```text
FUNCTION cacheGet(id):

  key = cacheKey(id)

  // 1️⃣ Check LRU (fastest)
  IF LRU contains key
    RETURN { source: "lru", value }

  // 2️⃣ Check Redis
  value = Redis.GET(key)

  IF value exists
    PARSE value
    PUT value into LRU
    RETURN { source: "redis", value }

  // 3️⃣ Cache miss
  RETURN { source: "miss", value: null }
```

---

### Set Cache (Write-Through)

```text
FUNCTION cacheSet(id, value, ttl):

  key = cacheKey(id)

  Redis.SET(key, value, TTL = ttl)

  LRU.SET(key, value)

  PUBLISH "cache-invalidate" event with id
```

---

### Delete Cache

```text
FUNCTION cacheDelete(id):

  key = cacheKey(id)

  LRU.DELETE(key)
  Redis.DELETE(key)

  PUBLISH "cache-invalidate" event with id
```

---
