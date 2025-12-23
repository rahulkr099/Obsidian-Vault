## 8. Fallback Strategy (WOW ⭐)

```
IF Redis is unavailable

  Use local in-memory counter
    - Fixed short window
    - Best-effort protection

  This keeps service available
  Even if global limit is briefly exceeded
```

👉 **Trade-off explained clearly**:  
Availability is preferred over strict correctness when Redis is down.