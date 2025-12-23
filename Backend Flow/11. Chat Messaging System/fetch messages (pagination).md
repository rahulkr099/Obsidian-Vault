## 14. Fetch Messages (Pagination)

```
WHEN GET /conversations/:id/messages

  Validate conversationId

  Fetch messages:
    conversationId
    ordered by createdAt
    limited by page size

  RETURN messages
```
