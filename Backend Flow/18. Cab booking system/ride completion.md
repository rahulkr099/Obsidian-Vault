## 9. Ride Completion

```
WHEN POST /rides/:rideId/complete

  Update ride status = "completed"

  Mark driver isAvailable = true

  Emit socket event:
    "ride:completed"

  RETURN updated ride
```
