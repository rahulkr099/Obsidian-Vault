## 📦 2. Data Models (Logical)

### PaymentIntent

```text
Payment:
  id
  amount
  currency
  status
  description
  metadata
  clientSecret
  createdAt
  updatedAt
  refunds[]
```

### Refund

```text
Refund:
  id
  paymentId
  amount
  status
  createdAt
```

---
