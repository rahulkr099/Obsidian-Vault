### 🔍 Validation Checks (Very Important)

```
IF currentDate > coupon.expiryDate
  RETURN error "Coupon expired"

IF orderValue < coupon.minOrderValue
  RETURN error "Order value too low"

IF coupon.usedCount >= coupon.usageLimit
  RETURN error "Coupon usage limit exceeded"
```
