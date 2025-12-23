## 6. Matchmaking Flow

```
ON player joins queue:
  add player to waitingPlayers

IF waitingPlayers size >= 2:
  playerA = dequeue
  playerB = dequeue
  create room
  assign playerA → 'X'
  assign playerB → 'O'
  notify both players
```
