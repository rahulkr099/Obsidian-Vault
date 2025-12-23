## 3. Data Structures (In-Memory)

### Notification Record

```
NOTIFICATION
  id
  channel (email | sms)
  recipient
  messageBody
  status (queued | sending | delivered | failed | scheduled)
  attempts
  nextAttemptTime
  idempotencyKey
  lastError
  createdAt
```

### Supporting Stores

```
notificationsMap     → id → notification
idempotencyMap       → idempotencyKey → id
queue                → list of notification ids
rateTracker          → channel → timestamps
metrics              → counters
```
