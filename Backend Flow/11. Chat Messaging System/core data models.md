## 3. Core Data Models

### User

```
USER
  id
  username
  displayName
  lastSeen
```

---

### Conversation

```
CONVERSATION
  id
  participants [userId]
  isGroup
  createdAt
  updatedAt
```

---

### Message

```
MESSAGE
  id
  conversationId
  senderId
  body
  status (sent | delivered | read)
  createdAt
```
