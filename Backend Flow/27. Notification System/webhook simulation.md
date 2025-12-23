## 10. Webhook Simulation

```
ON delivery or failure

  Emit event

  IF callback URL exists
    LOG "Webhook would be sent"
```

(In real systems → retryable HTTP POST with signatures)
