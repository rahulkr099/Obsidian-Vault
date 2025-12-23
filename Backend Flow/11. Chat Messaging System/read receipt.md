## 10. Read Receipt (Optional Wow)

```
WHEN user opens conversation

  Send ack:
    messageId
    status = "read"
```

```
Server updates message status
Broadcasts updated status
```
