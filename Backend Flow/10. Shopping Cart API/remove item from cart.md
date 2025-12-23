## 7. Remove Item from Cart

```
INPUT: userId, productId, quantity(optional)

Find user's open cart

IF item not in cart
  Return error

IF quantity >= current quantity
  Remove item
ELSE
  Reduce quantity

Save cart
Recalculate totals
Return updated cart
```
