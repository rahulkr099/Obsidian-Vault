## 5️⃣ Discount Calculation Logic

```
IF coupon.type == "percentage":
  discount = (orderValue * coupon.value) / 100
  discount = MIN(discount, coupon.maxDiscount)

ELSE IF coupon.type == "flat":
  discount = coupon.value
```
