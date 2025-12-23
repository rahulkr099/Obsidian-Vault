## 8. Return Book

```
WHEN POST /loans/return

  Find loan by loanId

  IF loan not found OR already returned
    RETURN error

  Mark returnedAt = now

  IF returnedAt > dueAt
    Calculate fine
    Set status = overdue
  ELSE
    Set status = returned

  Save loan

  Increase book.availableCopies by 1

  Log audit action: "return"

  TRY reservation promotion
```
