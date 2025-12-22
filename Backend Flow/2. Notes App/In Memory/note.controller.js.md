# 🎮 CONTROLLER — IN-MEMORY (PSEUDOCODE)

```
START NoteController

FOR create request
    CALL service.create
    SEND response

FOR getAll request
    CALL service.getAll with query params
    SEND response

FOR getById request
    CALL service.getById
    IF null → send 404
    ELSE send note

FOR update request
    CALL service.update
    IF null → send 404
    ELSE send updated note

FOR delete request
    CALL service.delete
    IF false → send 404
    ELSE confirm deletion

END NoteController
```

💬

> “Controllers are thin. All logic lives in services.”