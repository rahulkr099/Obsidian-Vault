## 🔥 8. Cache Warming (Cold-Start Optimization)

```text
FUNCTION warmCache():

  items = DB.LIST_ALL()

  FOR each item in items
    cacheSet(item.id, item, LONG_TTL)
```
