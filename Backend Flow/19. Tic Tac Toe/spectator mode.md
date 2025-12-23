## 14. Spectator Mode

```
EVENT spectate(roomId):
  IF room exists
    join socket room
    send current game snapshot
```
