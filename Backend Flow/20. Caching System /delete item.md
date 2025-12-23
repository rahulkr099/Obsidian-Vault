## 🗑️ 7. DELETE Item

```text
FUNCTION deleteItem(id):

  success = DB.DELETE(id)

  IF success
    cacheDelete(id)

  RETURN success
```
