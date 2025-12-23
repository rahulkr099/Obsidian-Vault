## 9. Batching (Throughput Optimization ⭐)

```
FOR each channel

  Take up to BATCH_MAX_SIZE notifications
  Send them sequentially respecting rate limit
```
