## ⚡ 10. Real-Time Updates (WOW)

```text
ON score update:

  oldRank = previous rank
  newRank = current rank

  IF change affects Top-N:
    BROADCAST leaderboard update via WebSocket
```
