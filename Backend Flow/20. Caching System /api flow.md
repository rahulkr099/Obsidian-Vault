## 🧪 10. API Flow Summary

```text
GET /items/:id
  → LRU
  → Redis
  → DB
  → Cache result

POST /items
  → DB
  → Cache set

DELETE /items/:id
  → DB
  → Cache delete
```
