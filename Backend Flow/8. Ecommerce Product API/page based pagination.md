## 9. Page-Based Pagination Flow

```
IF cursor is NOT provided

  Calculate skip = (page - 1) * limit

  Fetch products using:
    - filter
    - projection
    - sorting
    - skip
    - limit

  Count total matching products

  Calculate total pages

  Build pagination navigation links
    - previous page
    - next page

  Set response headers
    - X-Total-Count
    - X-Total-Pages
    - Link
    - ETag

  IF facets enabled
    Run aggregation to calculate:
      - category counts
      - brand counts
      - price statistics

  RETURN page info + products + facets
```
