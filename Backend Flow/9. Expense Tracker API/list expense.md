## 8. List Expenses (Pagination + Filters)

```
WHEN GET /expenses

  REQUIRE authenticated user

  Build filter:
    userId = logged-in user

  IF search query exists
    filter by description OR category OR tags

  IF category filter exists
    filter by category

  IF startDate / endDate exists
    filter by date range

  Apply pagination:
    skip = (page - 1) * limit
    limit = limit

  Sort by date descending

  Fetch expenses

  Count total records

  RETURN expenses + pagination metadata
```
