## 12. Rematch Flow

```
EVENT rematch_request:
  add player to rematchVotes

IF rematchVotes count == 2:
  reset game
  clear rematchVotes
  broadcast new game
```
