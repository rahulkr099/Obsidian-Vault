## 1. Application Startup (app.js)

```
START SERVER

Load required libraries
  - Express
  - Security middleware
  - Logging middleware
  - Compression middleware
  - Database connector

Create Express application

Apply global middlewares
  - Security headers
  - JSON body parsing
  - Response compression
  - Request logging

Connect to MongoDB database

Register routes
  - "/api/products" → Product routes

Define health check route "/"
  - Return server status

Start server on given PORT
  - Log server running message

END
```
