## 4. Create Event

```
WHEN POST /events

  Validate required fields:
    title, date, totalSeats

  Set availableSeats = totalSeats

  Save event to database

  RETURN created event
```
