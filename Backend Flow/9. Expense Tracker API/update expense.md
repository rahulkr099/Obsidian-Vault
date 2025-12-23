## 10. Update Expense

```
WHEN PUT /expenses/:id

  REQUIRE authenticated user

  Validate expenseId

  Allow updates only for:
    amount, category, description, date, tags, currency

  Update expense where:
    expenseId AND userId

  IF not found
    RETURN 404

  RETURN updated expense
```
