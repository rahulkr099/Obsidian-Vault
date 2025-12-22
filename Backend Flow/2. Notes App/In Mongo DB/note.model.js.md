# 🧩 MODEL — MONGODB NOTE MODEL (PSEUDOCODE)

```
START NoteSchema

DEFINE fields:
    title (required, trimmed, max length)
    content (required, trimmed)
    tags (array of strings)
    isDeleted (boolean, default false)
    versionHistory (array of old versions)

ENABLE automatic timestamps

CREATE text index on title + content

EXPORT Note model

END NoteSchema
```

💬

> “I added soft delete and version history for safety and auditability.”
