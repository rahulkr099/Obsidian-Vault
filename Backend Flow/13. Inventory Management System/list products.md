## 6. List Products (Search + Pagination)

```
WHEN GET /products

  Build filter:
    isDeleted = false
    IF search query exists
      filter name contains search term
    IF sku exists
      filter by sku

  Get pagination values

  Fetch total count

  Fetch paginated products sorted by latest update

  RETURN total count and product list
```
