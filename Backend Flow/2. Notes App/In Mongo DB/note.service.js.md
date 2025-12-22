# 🧠 SERVICE LAYER — MONGODB VERSION (PSEUDOCODE)

```
START MongoNoteService

FOR create
    INSERT note document into DB

FOR getAll
    BUILD query where isDeleted = false
    APPLY search and tag filters
    RETURN results

FOR getById
    VALIDATE ObjectId
    FIND note by ID and not deleted

FOR update
    FETCH note
    PUSH current state into versionHistory
    UPDATE fields
    SAVE note

FOR delete
    MARK note as isDeleted = true
    SAVE

END MongoNoteService
```

💬

> “Service layer is DB-agnostic. Only implementation changes.”