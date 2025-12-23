## 10. Get Single Product API

```
FUNCTION getProductById(request, response)

  Fetch product by ID

  IF product not found
    Return 404 error

  Generate ETag for caching

  Return product data

END FUNCTION
```
