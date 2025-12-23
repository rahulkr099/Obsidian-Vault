## 6. Driver Accepts Ride (Concurrency-Safe ⭐)

```
WHEN POST /rides/accept

  Try to update Ride where:
    rideId matches
    status is "requested"
    driver is null

  ATOMICALLY:
    set driverId
    set status = "assigned"

  IF update fails
    RETURN error "Ride already taken"

  Mark driver isAvailable = false

  Notify rider via socket:
    "ride:assigned"

  RETURN assigned ride
```

⭐ **Big interview win:**  
This prevents **two drivers accepting the same ride**.