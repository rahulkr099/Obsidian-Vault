## 7. Get Single Product

```
WHEN GET /products/:id

  Find product by id AND isDeleted = false

  IF not found
    RETURN 404

  RETURN product
```
