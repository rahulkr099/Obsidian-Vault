## 7. Join / Leave Conversation

```
WHEN client sends join_conversation(conversationId)

  Add socket to room = conversationId
```

```
WHEN client sends leave_conversation(conversationId)

  Remove socket from room
```
