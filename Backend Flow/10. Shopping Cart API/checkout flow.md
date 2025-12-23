## 10. Checkout Flow ⭐ (Most Important)

### Checkout (Idempotent + Safe)

```
INPUT: userId, idempotencyKey

Get user's open cart

IF cart already checked out with same idempotencyKey
  Return existing order

BEGIN TRANSACTION

FOR each item in cart
  IF product.stock < item.qty
    ABORT transaction
    Return error

FOR each item in cart
  Decrease product.stock by item.qty

Compute final total

Create order from cart

Mark cart as checked_out
Save idempotencyKey

COMMIT transaction

Return order
```

⭐ **Interview gold points**

- Prevents duplicate orders
    
- Prevents overselling
    
- Safe under concurrency
    
