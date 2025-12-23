## 11. Cancel Reservation

```
WHEN POST /reservations/:id/cancel

  Update reservation status to cancelled

  Log audit action: "cancel_reservation"

  RETURN updated reservation
```
