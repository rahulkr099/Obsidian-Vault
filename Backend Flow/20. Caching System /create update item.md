## ✍️ 6. CREATE / UPDATE Item

```text
FUNCTION upsertItem(data):

  item = DB.UPSERT(data)

  // Keep cache fresh immediately
  cacheSet(item.id, item, TTL)

  RETURN item
```
