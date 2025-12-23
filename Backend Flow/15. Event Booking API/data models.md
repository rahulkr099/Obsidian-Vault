## 3. Data Models

### Event

```
EVENT
  id
  title
  description
  date
  totalSeats
  availableSeats
  metadata (category, location)
  createdAt
```

### Booking

```
BOOKING
  id
  eventId
  user (name, email)
  status (CONFIRMED | CANCELLED | HOLD)
  idempotencyKey
  createdAt
```
