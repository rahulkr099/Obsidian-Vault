## 8. Join Matchmaking

```
EVENT join_queue:
  IF player already in room OR queue
    IGNORE
  ADD player to waitingPlayers
  TRY matchmaking
```
