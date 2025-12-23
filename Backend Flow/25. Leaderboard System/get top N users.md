## 🏆 4. Get Top-N Users

```text
FUNCTION getTopN(leaderboardName, N):

  key = "leaderboard:" + leaderboardName

  results = REDIS.ZREVRANGE(key, 0, N-1, WITH_SCORES)

  rank = 1
  FOR each (userId, score) in results:
    ADD { userId, score, rank } to response
    rank = rank + 1

  RETURN response
```
