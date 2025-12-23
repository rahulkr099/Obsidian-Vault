## 🔄 8. Durability (Optional but Smart)

```text
ON score update:

  WRITE to Redis (fast)
  PUSH event to queue

WORKER:
  READ event
  SAVE to DB (history / audit)
```
