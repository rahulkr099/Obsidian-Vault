## 7. Simulated Delivery Logic

```
SEND notification using simulated transport

  RANDOMLY decide:
    - success
    - transient failure

  IF success
    status = delivered
    record delivery time
    increment metrics.delivered

  IF failure
    HANDLE retry
```
