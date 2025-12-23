## 7. Decision Handling

```
IF allowed
  Allow request to continue
  Set response headers:
    - Rate limit
    - Remaining tokens
    - Reset estimate

ELSE
  Reject request
  Return HTTP 429 (Too Many Requests)
```
