## 🕹️ 8. Move Token Event

```text
ON socket event "move-token":

  IF socket.id != currentTurnPlayerId
    REJECT (cheat)

  IF no dice rolled
    REJECT

  APPLY moveToken()
  APPLY checkKill()

  LOG event "token-moved"

  advanceTurn()

  RESET lastDiceValue

  BROADCAST "game-state-updated"
  BROADCAST "turn-changed"
```
