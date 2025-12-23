## 3. Product Data Model (Schema)

```
DEFINE Product Schema
  Fields:
    - name
    - description
    - price
    - category
    - brand
    - rating
    - ratingCount
    - stock
    - tags
    - createdAt

Add indexes
  - Text index for search (name, description, brand)
  - Index on price
  - Compound index on (category, price)

EXPORT Product Model
```
