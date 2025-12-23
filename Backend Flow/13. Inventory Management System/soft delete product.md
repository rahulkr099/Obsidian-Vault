## 9. Soft Delete Product

```
WHEN DELETE /products/:id

  Mark product as isDeleted = true

  IF product not found
    RETURN 404

  RETURN success
```
