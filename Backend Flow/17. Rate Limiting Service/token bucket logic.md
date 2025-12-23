## 6. Token Bucket Logic (Core Algorithm ⭐)

```
FUNCTION tokenBucket(key, capacity, refillRate, now, requestedTokens)

  IF key does not exist
    tokens = capacity
    lastTimestamp = now

  ELSE
    Load tokens and lastTimestamp

  elapsedTime = now - lastTimestamp
  tokensToAdd = elapsedTime * refillRate

  tokens = min(capacity, tokens + tokensToAdd)

  IF tokens >= requestedTokens
    tokens -= requestedTokens
    allowed = true
  ELSE
    allowed = false

  Save updated tokens and timestamp to Redis
  Set TTL so unused keys auto-expire

  RETURN allowed, remainingTokens
END FUNCTION
```

👉 **Important:**  
This logic runs **atomically inside Redis**, so no race conditions even with many servers.