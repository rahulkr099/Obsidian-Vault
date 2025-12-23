## 13. Analytics — Category Breakdown ⭐

```
WHEN GET /expenses/analytics/categories

  REQUIRE authenticated user

  Optional date filters

  Filter expenses by:
    userId
    date range (optional)

  Group by category:
    sum(amount)
    count(expenses)

  Sort by total amount descending

  RETURN category summary
```
