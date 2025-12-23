## 5️⃣ Dice Roll Flow (Core Logic ⭐)

```
ON dice_roll(playerId):

  IF playerId ≠ TURN_ORDER[CURRENT_TURN_INDEX]
    SEND error "Not your turn"
    RETURN

  dice = RANDOM number between 1 and 6

  newPosition = PLAYERS[playerId].position + dice

  IF newPosition > 100
    newPosition = old position   // must land exactly on 100
```
