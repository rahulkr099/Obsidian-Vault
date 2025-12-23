## 5. Request Flow (Middleware)

```
ON every incoming request

  Identify caller
    - API key OR user id OR IP address

  Build Redis key using identifier + route

  Get current timestamp

  Call Redis Lua script with:
    - capacity (max tokens)
    - refill rate (tokens per second)
    - current time
    - tokens requested (usually 1)
```
