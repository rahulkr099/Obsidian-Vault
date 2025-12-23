## 4. Data Stored in Redis

```
FOR EACH identifier (userId / apiKey / IP):

Redis Key: rate:{identifier}:{route}

FIELDS:
- tokens        → current available tokens
- lastTimestamp → last refill time
```
