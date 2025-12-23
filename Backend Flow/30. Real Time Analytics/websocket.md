## ⚡ 4. WebSocket (Real-Time Updates)

```text
ON client WebSocket connection:
  LOG "Client connected"

ON event increment:
  BROADCAST "update" to all clients
```
