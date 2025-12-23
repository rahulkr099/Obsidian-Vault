## 📦 2. Counter Store (Memory + Redis Optional)

```text
INITIALIZE counters as empty map

INITIALIZE redisClient as null

FUNCTION initRedis():
  TRY
    connect to Redis
    set redisClient
  CATCH
    use in-memory counters
```

---

### ➕ Increment Event Counter

```text
FUNCTION incrementEvent(eventName):

  IF redisClient exists
    newCount = Redis.INCR(eventName)
  ELSE
    counters[eventName] = counters[eventName] + 1 (default 0)
    newCount = counters[eventName]

  RETURN newCount
```

---

### 🔍 Get Single Event Count

```text
FUNCTION getEvent(eventName):

  IF redisClient exists
    RETURN Redis.GET(eventName) OR 0
  ELSE
    RETURN counters[eventName] OR 0
```

---

### 📊 Get All Events

```text
FUNCTION getAllEvents():

  IF redisClient exists
    keys = Redis.GET_ALL_KEYS
    FOR each key
      result[key] = Redis.GET(key)
    RETURN result
  ELSE
    RETURN counters
```
