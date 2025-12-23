## 8. Sending a Message (Core Flow ⭐)

```
WHEN client sends send_message
  INPUT: conversationId, body, tempId

  Create new message:
    senderId = current user
    status = "sent"
    createdAt = now

  Save message to database

  Emit to all users in conversation room:
    event: "message"
    payload: message

  Emit back to sender:
    event: "message_ack"
    payload: { tempId, message }
```

⭐ **Why this is impressive**  
Supports optimistic UI using `tempId`.
