### 👤 User-level Usage Check

```
userUsage = FIND coupon.usedBy WHERE userId matches

IF userUsage exists AND userUsage.count >= coupon.userLimit
  RETURN error "User coupon limit exceeded"
```
