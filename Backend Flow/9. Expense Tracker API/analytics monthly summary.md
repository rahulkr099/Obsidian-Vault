## 12. Analytics — Monthly Summary ⭐

```
WHEN GET /expenses/analytics/monthly

  REQUIRE authenticated user

  Read year (default = current year)

  Filter expenses:
    userId
    date between Jan 1 and Dec 31 of year

  Group by month:
    sum(amount)
    count(expenses)

  Fill missing months with zero values

  RETURN array of 12 months
```

⭐ **Why this is impressive:**  
Shows aggregation, business logic, and data completeness.
