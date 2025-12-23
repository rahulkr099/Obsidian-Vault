## 6. Helper Logic — Parse Sorting

```
FUNCTION parseSort(sortString)

  IF sortString is empty
    Sort by newest first

  Split sortString by commas

  FOR each field
    IF field starts with "-"
      Sort descending
    ELSE
      Sort ascending

  RETURN sort object

END FUNCTION
```
