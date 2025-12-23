## 3. Core Data Models

### Driver

```
DRIVER
  id
  name
  phone
  isAvailable
  location (latitude, longitude)
  rating
```

### Ride

```
RIDE
  id
  riderName
  riderPhone
  pickupLocation
  dropoffLocation
  status (requested | assigned | ongoing | completed | cancelled)
  driverId
  fare
  surgeFlag
  requestedAt
```
