## 🔁 3. Update Score (SET or INCREMENT)

```text
FUNCTION updateScore(leaderboardName, userId, score, operation):

  key = "leaderboard:" + leaderboardName

  IF operation == "incr":
    newScore = REDIS.ZINCRBY(key, score, userId)
  ELSE:
    REDIS.ZADD(key, score, userId)
    newScore = score

  // (optional) persist event asynchronously to DB

  RETURN newScore
```
