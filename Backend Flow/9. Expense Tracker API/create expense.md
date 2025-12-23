## 7. Create Expense

```
WHEN POST /expenses

  REQUIRE authenticated user

  IF amount OR category missing
    RETURN error

  Create expense with:
    userId from token
    amount, category, description, date, tags

  Save expense

  RETURN created expense
```
