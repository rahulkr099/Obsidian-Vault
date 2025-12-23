## 13. Undo Flow (Optional WOW)

```
EVENT offer_undo:
  notify opponent

EVENT accept_undo:
  game.undoLastMove()
  broadcast updated board
```
