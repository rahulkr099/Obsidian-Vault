## 4. Routing Layer

```
WHEN request comes to "/api/products"
  CALL getProducts controller

WHEN request comes to "/api/products/:id"
  CALL getProductById controller
```
