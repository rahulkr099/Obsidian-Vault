## 15. Recurring Expense (Stub)

```
IF expense.recurring exists

  Background job runs daily

  IF today matches recurring rule
    AND today <= recurring.until

    Create new expense instance
```

(You can explain this without implementing — interviewers like this thinking.)
