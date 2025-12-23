## 🏠 3. Create / Join Room

```text
FUNCTION createRoom(roomId):
  room.players = empty list
  room.currentTurnPlayerId = null
  room.lastDiceValue = null
  room.eventLog = empty list
  room.status = "waiting"
  RETURN room
```

```text
ON socket event "join-room":

  IF room does not exist
    CREATE room

  IF room.players >= maxPlayers
    REJECT join

  ADD new player with 4 closed tokens

  IF players count >= 2 AND game not started
    SET currentTurnPlayerId = first player
    SET status = "playing"

  BROADCAST "player-joined" with room state
```
