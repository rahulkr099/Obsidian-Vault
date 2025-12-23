## 🚀 3. REST API Layer

---

### 📌 POST /event/:name — Increment Event

```text
FUNCTION handleIncrementEvent(request, response):

  eventName = request.params.name

  APPLY rate limit check

  count = incrementEvent(eventName)

  EMIT WebSocket event "update"
    payload: { eventName, count }

  RETURN response with eventName and count
```

---

### 📌 GET /event/:name — Get One Counter

```text
FUNCTION handleGetEvent(request, response):

  eventName = request.params.name

  count = getEvent(eventName)

  RETURN response with eventName and count
```

---

### 📌 GET /events — Get All Counters

```text
FUNCTION handleGetAllEvents(request, response):

  events = getAllEvents()

  RETURN response with events
```
