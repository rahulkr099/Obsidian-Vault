## 9. Message Delivery Acknowledgement ⭐

```
WHEN receiver gets message

  Send ack:
    messageId
    status = "delivered"
```

```
WHEN server receives ack

  Update message status in database

  Broadcast to conversation:
    event: "message_status_update"
```

---
