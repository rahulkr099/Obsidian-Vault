## 11. Error Handling

```
IF pickup or dropoff missing
  RETURN 400

IF no nearby drivers
  RETURN "searching"

IF ride already accepted
  RETURN 409

IF ride not found
  RETURN 404
```
