## ⚡ 7. WebSocket (Real-Time Updates)

```text
ON WebSocket client connect:
  SEND welcome message

FOR each queue event (waiting, active, progress, completed, failed):
  BROADCAST event + job data to all connected clients
```
