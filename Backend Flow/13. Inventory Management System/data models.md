## 3. Data Models

### Product Model

```
PRODUCT
  id
  name
  sku (unique)
  description
  price
  quantity
  minStock
  isDeleted
  metadata
  version (for optimistic locking)
  createdAt
  updatedAt
```

### Inventory Transaction Model

```
INVENTORY_TRANSACTION
  id
  productId
  type (IN | OUT | ADJUSTMENT | RESERVE | RELEASE)
  quantity
  note
  metadata
  createdAt
```
