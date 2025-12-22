# 🧩 MODEL — IN-MEMORY NOTE MODEL (PSEUDOCODE)

### `note.model.js`

```
START NoteModel

WHEN a new Note is created
    GENERATE unique ID
    SET title
    SET content
    SET tags (default empty)
    SET createdAt = current time
    SET updatedAt = current time
    SET isDeleted = false
    INITIALIZE versionHistory as empty list

END NoteModel
```

💬 **Explain to interviewer**

> “This class represents the shape of a note. It’s independent of storage, so I can later swap in MongoDB easily.”
