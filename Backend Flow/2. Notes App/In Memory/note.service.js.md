# 🧠 SERVICE LAYER — IN-MEMORY (CORE LOGIC)

### `note.service.js`

## Create Note

```
START createNote

CREATE new Note object using input data
STORE note in memory using note.id as key
RETURN created note

END createNote
```

---

## Get All Notes (Search + Filter)

```
START getAllNotes

FETCH all notes from memory
REMOVE notes where isDeleted = true

IF search query exists
    FILTER notes where title OR content contains query

IF tag filter exists
    FILTER notes that contain the tag

RETURN filtered notes list

END getAllNotes
```

---

## Get Note by ID

```
START getNoteById

FIND note using ID
IF note does not exist OR is deleted
    RETURN null

RETURN note

END getNoteById
```

---

## Update Note (With Versioning)

```
START updateNote

FIND note by ID
IF note does not exist OR is deleted
    RETURN null

SAVE current title and content into versionHistory

UPDATE provided fields only
UPDATE updatedAt timestamp

RETURN updated note

END updateNote
```

---

## Soft Delete Note

```
START deleteNote

FIND note by ID
IF note does not exist OR already deleted
    RETURN false

SET isDeleted = true
RETURN true

END deleteNote
```

💬

> “I used soft delete so data can be restored or audited later.”
