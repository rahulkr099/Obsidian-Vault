## 7. Book Seat (Concurrency Safe ⭐)

```
WHEN POST /events/:eventId/book

  Validate user info (name, email)

  IF idempotencyKey exists
    IF booking with key already exists
      RETURN existing booking

  START database transaction

  TRY to decrement availableSeats by 1
    ONLY IF availableSeats > 0

  IF event not found or sold out
    ROLLBACK transaction
    RETURN 409 (sold out)

  Create booking record with status CONFIRMED

  COMMIT transaction

  Generate QR code for booking

  Emit real-time seat update via Socket.IO

  RETURN booking + QR
```

👉 **Why this works**:  
Atomic update ensures **no two users can book the same last seat**.