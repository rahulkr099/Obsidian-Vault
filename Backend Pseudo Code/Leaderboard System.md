Perfect 👍  
Now let’s **compress the Leaderboard (Top-N Scores) system into clean, interview-ready PSEUDOCODE** that you can **write fast, explain clearly, and scale mentally**.

Simple words. Clear flow. Real system thinking.

---

# 🧠 Leaderboard System (Top-N Scores) — **PSEUDOCODE**

---

## 🧱 1. Core Components

```text
Components:
- API Server
- Redis Sorted Set (main leaderboard)
- Durable Store (optional: DB for history)
- Rank Calculator
```

---

## 📦 2. Data Structures

### Redis Sorted Set

```text
Key: leaderboard:<name>

Member: userId
Score: numeric score
```

Example:

```text
leaderboard:global
  userA → 1200
  userB → 980
```

---

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

---

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

---

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

---

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

---

## 🌍 7. Time-Based Leaderboards (Daily / Weekly)

```text
FUNCTION getLeaderboardKey(base, date):
  RETURN base + ":" + date

Example:
  leaderboard:daily:2025-12-14
  leaderboard:weekly:2025-W50
```

---

## 🔄 8. Durability (Optional but Smart)

```text
ON score update:

  WRITE to Redis (fast)
  PUSH event to queue

WORKER:
  READ event
  SAVE to DB (history / audit)
```

---

## ⚖️ 9. Tie-Breaking Strategy

```text
If two users have same score:
  1. Earlier updated wins
  OR
  2. Lexicographically smaller userId wins
```

(Explain this clearly in interview)

---

## ⚡ 10. Real-Time Updates (WOW)

```text
ON score update:

  oldRank = previous rank
  newRank = current rank

  IF change affects Top-N:
    BROADCAST leaderboard update via WebSocket
```

---

## 🛡️ 11. Security & Fairness

```text
- Validate score server-side
- Rate-limit score submissions
- Log suspicious jumps
```

---

## 🎯 Full Request Flow (Explain This)

```text
Client submits score
   ↓
Server validates request
   ↓
Redis updates sorted set
   ↓
(Optional) persist event
   ↓
Fetch Top-N or Rank instantly
```

---

## ⭐ Interview WOW Points to Say

> “Redis sorted sets give us log-time updates and fast Top-N queries.”

> “We separate fast reads (Redis) from durability (DB).”

> “Time-window leaderboards are just different Redis keys.”

---

## 🚀 Easy Extensions (Mention if Asked)

```text
- Friends-only leaderboard
- Region-based leaderboard
- Weekly reset + rewards
- Snapshot replay animation
- Badge system
```

---

## ⏱️ Why This Fits 1 Hour Perfectly

```text
- Simple data model
- Very little code
- High performance
- Easy to explain
- Scales naturally
```

---

If you want next 👇  
👉 **LLD / HLD diagrams**  
👉 **Concurrency & race-condition discussion**  
👉 **MongoDB-only version**  
👉 **Frontend leaderboard React component**

Just tell me 👍