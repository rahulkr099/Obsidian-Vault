## 📦 2. Data Models (Logical)

### Account

```text
Account:
  id
  balance
  version (optional, for optimistic locking)
```

### Ledger Entry (WOW factor)

```text
Ledger:
  transactionId
  fromAccount
  toAccount
  amount
  status (started | success | failed)
  timestamp
```
