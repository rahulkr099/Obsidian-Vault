## 5. List Books (Search + Filters + Pagination)

```
WHEN GET /books

  Read query params:
    page, limit, searchText, author, tags, sort

  Build filter object

  IF searchText exists
    Perform full-text search on title and author

  Fetch total count

  Fetch paginated books sorted by criteria

  RETURN total + book list
```
