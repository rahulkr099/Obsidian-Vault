## 📦 2. Data Structures

### Room State

```text
Room:
  roomId
  players[]
  currentTurnPlayerId
  lastDiceValue
  eventLog[]
  status (waiting | playing | finished)
```

### Player

```text
Player:
  id (socketId)
  name
  color
  tokens[]
```

### Token

```text
Token:
  position
  isOpen
  isFinished
```
