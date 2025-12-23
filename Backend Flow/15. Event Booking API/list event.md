## 5. List Events (Filter + Pagination)

```
WHEN GET /events

  Read query params:
    page, limit, category, location

  Build filter object dynamically

  Fetch events:
    - apply filters
    - sort by upcoming date
    - apply pagination

  RETURN list of events
```
