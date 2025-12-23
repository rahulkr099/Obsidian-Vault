## 8. Rider Checks ETA (Quick Calculation)

```
WHEN GET /rides/:rideId/eta

  Fetch ride and assigned driver

  IF no driver yet
    RETURN eta = null

  Calculate distance using Haversine formula

  Estimate ETA using average speed

  RETURN etaMinutes and distance
```
