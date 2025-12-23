## 9. Get Single Expense

```
WHEN GET /expenses/:id

  REQUIRE authenticated user

  IF expenseId invalid
    RETURN error

  Find expense by:
    expenseId AND userId

  IF not found
    RETURN 404

  RETURN expense
```
