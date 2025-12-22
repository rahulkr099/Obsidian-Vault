# 1️⃣ `package.json` — Project Metadata

### Purpose

Defines project name, dependencies, and run commands.

### Pseudocode

```
START package configuration

SET project name and version
DEFINE entry file for application

DEFINE scripts:
    start → run server
    dev → run server with auto-reload

LIST runtime dependencies:
    express, mongoose, jwt, bcrypt, joi, etc.

LIST development dependencies:
    nodemon

END package configuration
```

🗣 Interview line:

> “package.json defines how the app runs and what libraries it depends on.”
