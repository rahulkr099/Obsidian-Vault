## 9. Calculate Cart Totals (Reusable Logic)

```
SET subtotal = sum(item.qty × item.priceAtAdd)

IF coupon exists
  IF subtotal < coupon.minCartValue
    discount = 0
  ELSE IF coupon.type == percent
    discount = subtotal × (coupon.value / 100)
  ELSE
    discount = coupon.value

discount = min(discount, subtotal)

total = subtotal - discount

RETURN subtotal, discount, total
```

---
