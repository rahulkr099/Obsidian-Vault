# 4️⃣ `docker-compose.yml` — Multi-Service Setup

### Purpose

Runs backend + MongoDB together.

### Pseudocode

```
START docker compose

DEFINE app service:
    BUILD from Dockerfile
    MAP ports
    SET environment variables
    WAIT for database

DEFINE mongo service:
    USE official MongoDB image
    ENABLE persistent storage

DEFINE shared volume for database

END docker compose
```

🗣

> “docker-compose helps spin up app and database together.”