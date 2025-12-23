## 5. Rider Requests a Ride

```
WHEN POST /rides/request

  Read pickup and dropoff locations

  Create new Ride with:
    status = "requested"
    driver = null

  Find nearby drivers:
    - only drivers with isAvailable = true
    - within 5 km radius using geo query

  IF number of drivers is low
    mark ride as surge = true

  FOR each nearby driver
    Send real-time socket event "ride:request"

  RETURN rideId and nearby driver count
```

⭐ **Why this is good**  
Uses geospatial queries for fast matching.
