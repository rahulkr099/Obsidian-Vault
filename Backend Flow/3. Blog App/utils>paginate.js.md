# 1️⃣1️⃣ Pagination Utility — `utils/paginate.js`

### Purpose

Standardizes pagination logic.

### Pseudocode

```
FUNCTION getPagination:
    READ page from query
    READ limit from query
    CALCULATE skip value
    RETURN page, limit, skip

FUNCTION buildMeta:
    CALCULATE total pages
    RETURN pagination metadata
```

🗣

> “Pagination prevents loading large datasets at once.”