## 7. Borrow Book (Concurrency Safe ⭐)

```
WHEN POST /loans/borrow

  Read bookId and userId

  ATOMICALLY:
    Find book where availableCopies > 0
    Decrease availableCopies by 1

  IF no book found
    RETURN error "No copies available"

  Create loan record:
    borrowedAt = now
    dueAt = now + allowed days
    status = borrowed

  Log audit action: "borrow"

  RETURN loan details
```

👉 **Why this matters:**  
Prevents **two users borrowing the last copy at the same time**.
