## 2️⃣ Core Data Structures

### Coupon

```
COUPON {
  code
  type              // percentage | flat
  value
  minOrderValue
  maxDiscount
  expiryDate
  usageLimit
  usedCount
  userLimit
  usedBy[]          // list of { userId, count }
}
```
