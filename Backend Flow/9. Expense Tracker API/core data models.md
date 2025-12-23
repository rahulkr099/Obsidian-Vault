## 3. Core Data Models

### User

```
USER
  id
  name
  email
  passwordHash
  createdAt
```

### Expense

```
EXPENSE
  id
  userId
  amount
  currency
  category
  description
  date
  tags
  recurring (interval, until)
  createdAt
```
