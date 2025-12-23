## 🖥️ 5. Dashboard (Client Side Logic)

```text
ON page load:
  FETCH /events
  RENDER cards for each event with count

ON receiving WebSocket "update":
  IF event exists on UI
    update count
    play animation
  ELSE
    reload events
```
