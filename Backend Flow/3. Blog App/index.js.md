# 5️⃣ `src/index.js` — Application Entry Point

### Purpose

Starts the server after DB connection.

### Pseudocode

```
LOAD environment variables

IMPORT express app
IMPORT database connection function

READ port number

CONNECT to database
IF connection successful
    START server on port
ELSE
    LOG error
    EXIT process
```

🗣

> “Server starts only after database connection succeeds.”