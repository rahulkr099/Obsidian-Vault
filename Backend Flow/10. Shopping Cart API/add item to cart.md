## 6. Add Item to Cart

```
INPUT: userId, productId, quantity

IF product does not exist
  Return error

IF product stock < quantity
  Return "not enough stock"

Get user's open cart

IF product already in cart
  Increase quantity
ELSE
  Add new item with priceAtAdd = product.price

Save cart
Recalculate totals
Return updated cart
```

⭐ **Why priceAtAdd?**  
Protects cart from future price changes.
