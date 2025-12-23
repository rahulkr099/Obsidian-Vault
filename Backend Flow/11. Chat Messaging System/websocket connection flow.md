## 6. WebSocket Connection Flow

```
WHEN socket connects

  Read token from connection

  IF token invalid
    Reject connection

  ELSE
    Attach userId to socket
    Mark user as online
    Broadcast presence update
```
