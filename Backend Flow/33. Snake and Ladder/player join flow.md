## 4️⃣ Player Join Flow

```
ON player_connect(playerId):

  ADD playerId to PLAYERS with position = 0
  ADD playerId to TURN_ORDER

  BROADCAST updated PLAYERS to all clients
```
