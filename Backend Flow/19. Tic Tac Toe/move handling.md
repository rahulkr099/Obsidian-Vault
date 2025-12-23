## 10. Move Handling (Core Interview Part ⭐)

```
EVENT move(roomId, cellIndex):

  FIND room
  FIND game

  IF not player's turn
    reject move

  TRY:
    result = game.makeMove(cellIndex)
    broadcast updated game state

    IF result == winner
      update ratings
      broadcast game_over
  CATCH:
    send error
```
