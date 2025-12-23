## 🧮 5. Get User Rank

```text
FUNCTION getUserRank(leaderboardName, userId):

  key = "leaderboard:" + leaderboardName

  rankIndex = REDIS.ZREVRANK(key, userId)

  IF rankIndex is NULL:
    RETURN null

  score = REDIS.ZSCORE(key, userId)

  RETURN {
    rank: rankIndex + 1,
    score: score
  }
```