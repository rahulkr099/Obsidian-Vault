# 3️⃣ `Dockerfile` — Container Build Instructions

### Purpose

Creates a production-ready container image.

### Pseudocode

```
START Docker build

USE lightweight Node.js base image
SET working directory

COPY dependency files
INSTALL only production dependencies

COPY application source code

SET environment to production
EXPOSE application port

START server using node

END Docker build
```

🗣

> “Docker ensures consistent runtime across machines.”