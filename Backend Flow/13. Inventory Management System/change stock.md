## 10. Change Stock (Atomic + Transactional ⭐⭐)

```
WHEN POST /products/:id/stock

  Validate:
    type is allowed
    qty > 0

  START database transaction

  Find product (and match version if expectedVersion exists)

  IF product not found or version mismatch
    ABORT transaction
    RETURN 409

  CALCULATE new quantity:
    IF type is IN or RELEASE
      quantity += qty
    IF type is OUT or RESERVE
      IF quantity < qty
        ABORT transaction
        RETURN error
      quantity -= qty
    IF type is ADJUSTMENT
      quantity = qty

  Save updated product

  Create inventory transaction record

  COMMIT transaction

  IF quantity <= minStock
    Flag low stock

  RETURN updated product + low-stock flag
```

👉 **Why this is powerful:**  
Product quantity and transaction log are always consistent.
