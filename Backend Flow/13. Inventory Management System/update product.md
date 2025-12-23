## 8. Update Product (Optimistic Locking ⭐)

```
WHEN PATCH /products/:id

  Remove quantity field from update (not allowed here)

  IF expectedVersion provided
    Update product ONLY IF id AND version match
    IF no record updated
      RETURN 409 (version conflict)
  ELSE
    Update product normally

  RETURN updated product
```

👉 **Why this matters:** prevents lost updates when multiple users edit the same product.
