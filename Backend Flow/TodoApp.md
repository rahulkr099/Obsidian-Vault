```
## Endpoints

- `POST /todos` - Create todo
- `GET /todos` - List todos (filters: status, tag, q, page, limit, sortBy)
- `GET /todos/:id` - Get todo
- `PATCH /todos/:id` - Update todo (partial)
- `PATCH /todos/:id/complete` - Mark complete
- `DELETE /todos/:id` - Soft delete
- `POST /todos/:id/restore` - Restore soft-deleted todo
- `GET /todos/stats` - Simple stats aggregation
```
# app.js
```
START

IMPORT Express framework
IMPORT async error handler helper
IMPORT todo routes
IMPORT centralized error handler

CREATE Express application

ENABLE JSON body parsing middleware

REGISTER "/todos" routes

CREATE "/healthz" route
    WHEN route is called
        RETURN { ok: true }

HANDLE unknown routes
    IF route does not exist
        RETURN 404 with "Route not found"

REGISTER centralized error handler

EXPORT Express application

END

```
# server.js
```
START

IMPORT mongoose library
IMPORT dotenv library
IMPORT Express app

LOAD environment variables

SET port number
SET MongoDB connection URL

DEFINE async function startServer
    TRY
        CONNECT to MongoDB
        PRINT "Connected to MongoDB"

        START server on given port
        PRINT "Server running"

    CATCH error
        PRINT error message
        EXIT application

CALL startServer function

END

```
# Big Picture Flow (Easy to Remember)
```
Load configs
↓
Create Express app
↓
Attach middleware & routes
↓
Handle errors
↓
Connect database
↓
Start server

```
todo.routes.js
```
START

IMPORT Express framework
CREATE a router instance

IMPORT todo controller
IMPORT request validation functions

DEFINE route: POST "/"
    VALIDATE create request
    CALL controller to create a todo

DEFINE route: GET "/"
    CALL controller to list all todos

DEFINE route: GET "/stats"
    CALL controller to return todo statistics

DEFINE route: GET "/:id"
    EXTRACT todo id from request
    CALL controller to fetch single todo

DEFINE route: PATCH "/:id"
    VALIDATE update request
    CALL controller to update todo

DEFINE route: PATCH "/:id/complete"
    MARK the given todo as completed

DEFINE route: DELETE "/:id"
    SOFT DELETE the given todo

DEFINE route: POST "/:id/restore"
    RESTORE a previously deleted todo

EXPORT router

END

-----
Request comes in
↓
Route matches
↓
(Optional) Validation runs
↓
Controller handles logic
↓
Response sent back


```

# src/controller/todo.controller.js
### 1. create Todo
```
1. Fetch payload from req.body
2. Insert into DB 
3. Log into action
4. Return new todo
```
### 2. Get a Single Todo (not soft deleted)
```
1. Find a todo by ID if not deleted - using req.params.id
2. If no match found - return res.status 404 with error message
3. Return todo 
```
### 3. List Todos with filters, search, pagination and sorting
```
1. Fetch pagination, filtering, searching, sorting from req.query with default value
2. Base filters: fetch only active items
3. Filter by status if present
4. Filter by tags - comma separated
5. Build initial DB query
6. If search keyword present
   6(1) text search
   6(2) Order by relevance
7. Convert sortBy string into Mongo sort object
   7(1) Apply sorting
   7(2) Pagination skip
   7(3) Pagination limit
8. Run query + count in parallel for performance
9. Send response with required data
```
### 4. Convert "priority, -dueDate" into { priority: 1, dueDate : -1 }
```

```

