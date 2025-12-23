## 15. Disconnect Handling

```
ON disconnect:
  IF player in queue
    remove from queue

  IF player in room:
    notify opponent
    mark game finished
    opponent wins by forfeit
    update ratings
    clean up room
```
