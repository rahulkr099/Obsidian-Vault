## 8. Cancel Booking

```
WHEN POST /bookings/:bookingId/cancel

  START database transaction

  Find booking by id

  IF booking not found
    ROLLBACK
    RETURN 404

  IF booking already cancelled
    ROLLBACK
    RETURN error

  Mark booking status = CANCELLED

  Increment event.availableSeats by 1

  COMMIT transaction

  Emit real-time seat update

  RETURN success
```
