## 13. Error Handling Strategy

```
IF validation error
  RETURN 400

IF event sold out
  RETURN 409

IF not found
  RETURN 404

IF unexpected error
  RETURN 500
```
