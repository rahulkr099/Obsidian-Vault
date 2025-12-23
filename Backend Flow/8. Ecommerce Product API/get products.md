## 7. Get Products API (Main Logic)

```
FUNCTION getProducts(request, response)

  Read query parameters
    - page, limit
    - cursor
    - filters
    - sorting
    - text search
    - field selection
    - facet flag

  Build filter object using helper

  IF text search exists
    Add text search condition

  Build projection (selected fields)

  Build sort object

  IF cursor exists
    PERFORM cursor-based pagination
  ELSE
    PERFORM page-based pagination

END FUNCTION
```
