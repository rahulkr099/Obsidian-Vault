## 10. Create Reservation

```
WHEN POST /reservations

  Check if user already has active reservation
  IF yes
    RETURN error

  Create reservation with status = active

  Log audit action: "reserve"

  RETURN reservation
```
