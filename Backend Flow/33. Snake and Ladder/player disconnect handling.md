## 🔌 Player Disconnect Handling

```
ON player_disconnect(playerId):

  REMOVE playerId from PLAYERS
  REMOVE playerId from TURN_ORDER

  IF TURN_ORDER is empty
    RESET game

  BROADCAST updated PLAYERS
```
