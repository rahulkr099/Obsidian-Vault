## 3. Data Models

### Book

```
BOOK
  id
  title
  author
  isbn
  description
  totalCopies
  availableCopies
  tags
  publishedAt
  createdAt
```

### User

```
USER
  id
  name
  email
  role (member | librarian)
  createdAt
```

### Loan

```
LOAN
  id
  bookId
  userId
  borrowedAt
  dueAt
  returnedAt
  fine
  status (borrowed | returned | overdue)
```

### Reservation

```
RESERVATION
  id
  bookId
  userId
  reservedAt
  status (active | cancelled | fulfilled)
  notifiedAt
```

### Audit Log

```
AUDIT_LOG
  id
  action
  actor
  metadata
  createdAt
```

---
