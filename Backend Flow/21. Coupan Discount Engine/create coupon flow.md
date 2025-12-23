## 3️⃣ CREATE COUPON Flow

```
FUNCTION createCoupon(couponData):

  VALIDATE couponData fields

  IF coupon code already exists
    RETURN error "Coupon already exists"

  SAVE couponData in database

  RETURN success
```
