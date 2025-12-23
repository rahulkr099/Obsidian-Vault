## 14. Export Expenses as CSV ⭐

```
WHEN GET /expenses/export/csv

  REQUIRE authenticated user

  Apply same filters as list endpoint

  Fetch matching expenses

  Convert expenses to CSV rows:
    date, amount, currency, category, description, tags

  Set response headers:
    Content-Type = text/csv
    Content-Disposition = attachment

  RETURN CSV file
```
