## 8. Cursor-Based Pagination Flow

```
IF cursor is provided

  Decode cursor to timestamp

  Filter products created before cursor time

  Fetch limit + 1 products (to detect next page)

  IF extra product exists
    Remove extra product
    Generate next cursor from last product timestamp
  ELSE
    No more pages

  Set response headers
    - X-Result-Count
    - X-Next-Cursor (if exists)
    - ETag for caching

  IF facets enabled
    Run aggregation to calculate:
      - category counts
      - brand counts
      - price buckets

  RETURN products + next cursor + facets
```
