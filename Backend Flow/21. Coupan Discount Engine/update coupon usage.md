## 6️⃣ Update Coupon Usage (Atomic Thinking)

```
coupon.usedCount += 1

IF userUsage exists:
  userUsage.count += 1
ELSE:
  ADD { userId, count: 1 } to coupon.usedBy

SAVE coupon
```
