## 10. Socket.IO Room Strategy

```
ON socket connect

  IF driver connects
    Join room "driver:{driverId}"

  IF rider joins a ride
    Join room "ride:{rideId}"

Events:
  ride:request     → sent to drivers
  ride:assigned    → sent to rider
  driver:location  → sent to rider
  ride:completed   → sent to rider
```
