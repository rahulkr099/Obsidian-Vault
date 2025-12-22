# 7️⃣ `src/config/db.js` — Database Connection

### Purpose

Connects MongoDB using Mongoose.

### Pseudocode

```
READ database URI

CONNECT to MongoDB
IF connected
    LOG success message
ELSE
    THROW error
```

🗣

> “Database connection is isolated for clean startup logic.”