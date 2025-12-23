## 9. Reservation Auto-Promotion (WOW ⭐)

```
AFTER book return

  Find earliest active reservation for this book

  IF reservation exists
    Mark reservation as fulfilled
    Set notifiedAt = now

    Decrease availableCopies by 1
    (copy is now held for reserved user)

    Log audit action: "reservation_promoted"
```

👉 **Why this is impressive:**  
Shows FIFO handling + real-world library behavior.
