## 12. Presence Tracking

```
WHEN user connects
  Mark online
  Broadcast presence = online
```

```
WHEN user disconnects
  Mark offline
  Update lastSeen timestamp
  Broadcast presence = offline
```
