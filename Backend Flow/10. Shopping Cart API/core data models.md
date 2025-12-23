## 3. Core Data Models

### Product

```
PRODUCT
  id
  name
  price
  sku
  stock
```

---

### Cart

```
CART
  id
  userId
  items [
    productId
    quantity
    priceAtAdd
  ]
  couponId (optional)
  status (open | checked_out)
  idempotencyKey
```

---

### Coupon

```
COUPON
  code
  type (percent | fixed)
  value
  minCartValue
  expiryDate
```

---

### Order

```
ORDER
  id
  cartId
  userId
  items
  totalAmount
  status
```
