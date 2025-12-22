# 🎮 CONTROLLER — MONGODB (ASYNC)

```
START AsyncNoteController

TRY
    CALL service
    SEND success response
CATCH error
    LOG error
    SEND 500 response

END AsyncNoteController
```

💬

> “Async controllers with try-catch prevent server crashes.”