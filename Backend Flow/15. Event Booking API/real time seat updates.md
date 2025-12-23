## 10. Real-Time Seat Updates (WOW ⭐)

```
ON WebSocket connection

  IF client subscribes to eventId
    Join socket room for eventId

  IF seat count changes
    Emit "seat_update" to event room
```

👉 **Result**:  
All connected clients instantly see seat count changes.
