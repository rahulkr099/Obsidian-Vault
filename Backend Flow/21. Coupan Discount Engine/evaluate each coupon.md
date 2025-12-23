### 🔁 Evaluate Each Coupon

```
FOR each coupon IN coupons:

  IF coupon expired
    CONTINUE

  IF orderValue < coupon.minOrderValue
    CONTINUE

  CALCULATE discount using same logic as applyCoupon

  IF discount > bestDiscount:
    bestDiscount = discount
    bestCoupon = coupon
```
