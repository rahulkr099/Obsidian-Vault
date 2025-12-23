## 9️⃣ IDEMPOTENT APPLY (BONUS WOW ⭐)

```
FUNCTION applyCouponIdempotent(requestId, userId, couponCode):

  IF requestId already processed
    RETURN previous result

  ELSE
    result = applyCoupon(couponCode, orderValue, userId)
    STORE result with requestId
    RETURN result
```
