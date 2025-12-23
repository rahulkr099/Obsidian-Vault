## 🛡️ 8. Rate Limiting (Stability Feature)

```text
FOR each IP:
  allow max N requests per second
  IF limit exceeded
    RETURN error "Too many requests"
```
