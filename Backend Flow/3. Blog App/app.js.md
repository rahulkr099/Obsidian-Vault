# 6️⃣ `src/app.js` — Express Setup

### Purpose

Configures middleware and routes.

### Pseudocode

```
CREATE express application

ENABLE security headers
ENABLE CORS
ENABLE JSON request parsing
ENABLE request logging

REGISTER authentication routes
REGISTER post routes
REGISTER comment routes

DEFINE health check route

REGISTER centralized error handler (last)

EXPORT app
```

🗣

> “app.js wires middleware and routes together.”