## 👥 6. Get Users Around a Player (Neighbors)

```text
FUNCTION getAroundUser(leaderboardName, userId, k):

  key = "leaderboard:" + leaderboardName

  userRank = REDIS.ZREVRANK(key, userId)
  IF userRank is NULL:
    RETURN null

  start = max(0, userRank - k)
  end = userRank + k

  results = REDIS.ZREVRANGE(key, start, end, WITH_SCORES)

  FOR each result:
    CALCULATE rank = start + index + 1
    ADD { userId, score, rank }

  RETURN list
```
