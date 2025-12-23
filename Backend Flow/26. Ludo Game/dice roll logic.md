## 🎲 4. Dice Roll Logic (Cheat-Safe)

```text
FUNCTION rollDice():
  RETURN random number between 1 and 6
```

```text
ON socket event "roll-dice":

  IF socket.id != room.currentTurnPlayerId
    REJECT (cheat attempt)

  diceValue = rollDice()
  room.lastDiceValue = diceValue

  LOG event "dice-roll"

  BROADCAST "dice-rolled"
```
