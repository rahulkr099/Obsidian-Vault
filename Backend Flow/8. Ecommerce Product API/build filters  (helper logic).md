## 5. Helper Logic — Build Filters

```
FUNCTION buildFilter(queryParams)

  Initialize empty filter object

  IF category provided
    Add category condition

  IF brand provided
    Add brand condition

  IF tags provided
    Split tags and match any

  IF inStock is true
    Filter products with stock > 0

  IF minPrice or maxPrice provided
    Apply price range filter

  IF minRating provided
    Filter rating >= minRating

  RETURN filter object

END FUNCTION
```
