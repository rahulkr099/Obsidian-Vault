## 9. Create / Join Room

```
EVENT create_room:
  create empty room
  assign creator as player X

EVENT join_room(roomId):
  IF room exists AND has one player
    add second player
    start game
  ELSE
    reject
```
