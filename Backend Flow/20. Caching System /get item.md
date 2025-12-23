## 📥 5. GET Item (Cache-Aside Pattern)

```text
FUNCTION getItem(id):

  cached = cacheGet(id)

  IF cached.source != "miss"
    RETURN cached.value WITH cacheSource

  // Cache miss → DB hit
  item = DB.GET(id)

  IF item does not exist
    RETURN null

  cacheSet(id, item, TTL)

  RETURN item WITH source = "db"
```
