## 11. Delete Expense

```
WHEN DELETE /expenses/:id

  REQUIRE authenticated user

  Validate expenseId

  Delete expense where:
    expenseId AND userId

  IF not found
    RETURN 404

  RETURN success message
```
