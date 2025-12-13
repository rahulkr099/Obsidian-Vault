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
You’re doing great work here 👍  
This controller already looks **industry-ready**, so let’s turn it into **clean, easy pseudocode** that clearly explains _what happens_, not _how JavaScript works_.

---

## Pseudocode for `todo.controller.js`

### 1️⃣ Create Todo

```
START createTodo

READ request body as payload

SAVE payload into database as new todo

LOG activity:
    - store todo ID
    - action = "create"
    - store payload

SEND response:
    - status = 201 (created)
    - return created todo

END createTodo
```

---

### 2️⃣ Get Single Todo (not deleted)

```
START getTodo

READ todo ID from request parameters

SEARCH database for todo:
    - match ID
    - softDelete must be false

IF todo is NOT found
    SEND response:
        - status = 404
        - message = "Not found"
    STOP

SEND response:
    - return todo data

END getTodo
```

---

## Controller Flow (Simple View)

```
Request arrives
↓
Controller reads input
↓
Database operation
↓
Optional activity log
↓
Response sent back
```

---

## Smart Improvement Ideas 💡 (Thinking Ahead)

- 🔹 Add **try-catch at controller level**
    
    - For clearer custom error messages
        
- 🔹 Add **ObjectId validation**
    
    - Avoid MongoDB cast errors
        
- 🔹 Add **user context**
    
    - `createdBy`, `updatedBy`
        
- 🔹 Add **transaction support**
    
    - Todo + Activity in one atomic operation
        
- 🔹 Add **DTO / response formatter**
    
    - Keep response structure consistent
        

If you want, next we can:

- Write pseudocode for **list / update / delete**
    
- Convert this into **exam answer format**
    
- Improve it to **transaction-safe version**
    
- Explain this in **interview-style language**
    

Just say 👍 and we’ll keep going 🚀
Excellent 👌  
This is a **very strong real-world listing API**. Let’s convert it into **clean, simple pseudocode** that clearly explains the idea step by step.

---

## Pseudocode for **List Todos**

```
START listTodos

READ query parameters:
    page, limit, status, tag, searchText, sortBy
SET default values if not provided

CREATE base filter:
    softDelete = false

IF status is provided
    ADD status to filter

IF tag is provided
    SPLIT tags by comma
    FILTER todos that contain any of these tags

CREATE database query using filters

IF search text exists
    APPLY text search on todos
    SORT results by search relevance

CONVERT sortBy string into sorting rules

APPLY sorting to query
APPLY pagination:
    SKIP (page - 1) * limit
    LIMIT number of results

RUN in parallel:
    - execute todo query
    - count total matching todos

SEND response:
    - list of todos
    - metadata (total, page, limit)

END listTodos
```

---

## Pseudocode for **parseSort Helper**

```
START parseSort

SPLIT sortBy string by comma

FOR each field
    IF field starts with "-"
        SET field order to descending
    ELSE
        SET field order to ascending

RETURN sorting object

END parseSort
```

---

## Simple Flow Diagram 🧠

```
Read query params
↓
Build filters
↓
Apply search
↓
Apply sorting
↓
Apply pagination
↓
Fetch data + count
↓
Send response
```

---

## Smart Improvement Ideas 💡 (Future-Ready Thinking)

- 🔹 Add **max limit protection**
    
    - Prevent users from requesting huge data
        
- 🔹 Add **indexing strategy**
    
    - Text index + compound filters
        
- 🔹 Add **cursor-based pagination**
    
    - Faster than skip for large datasets
        
- 🔹 Add **cache layer**
    
    - Cache popular queries (Redis)
        
- 🔹 Add **query validation**
    
    - Reject invalid sort fields early
        

If you want, next we can:

- Write pseudocode for **update / delete**
    
- Convert this into **interview explanation**
    
- Design **cursor pagination version**
    
- Optimize this for **very large datasets**
    

Just say continue 🚀
You’re building this **exactly like a real production backend** 👏  
Let’s convert each part into **very clear, simple pseudocode**, keeping it **exam-friendly and interview-ready**.

---

## 1️⃣ Pseudocode — **Update Todo (Partial Update)**

```
START updateTodo

READ todo ID from request parameters
READ update data from request body

FIND todo by ID where:
    - not soft deleted

UPDATE todo:
    - set provided fields
    - increment version by 1
    - return updated document

IF todo not found
    SEND 404 error
    STOP

LOG activity:
    - action = "update"
    - store todo ID and payload

SEND updated todo in response

END updateTodo
```

---

## 2️⃣ Pseudocode — **Mark Todo as Completed**

```
START completeTodo

READ todo ID from request parameters

CREATE update object:
    - status = "done"
    - completedAt = current time

FIND todo by ID where:
    - not soft deleted

UPDATE todo:
    - apply update object
    - increment version by 1
    - return updated document

IF todo not found
    SEND 404 error
    STOP

LOG activity:
    - action = "complete"
    - store update data

SEND updated todo in response

END completeTodo
```

---

## 3️⃣ Pseudocode — **Soft Delete Todo**

```
START softDeleteTodo

READ todo ID from request parameters

FIND todo by ID where:
    - not soft deleted

UPDATE todo:
    - set softDelete = true
    - increment version by 1
    - return updated document

IF todo not found
    SEND 404 error
    STOP

LOG activity:
    - action = "delete"

SEND updated todo in response

END softDeleteTodo
```

---

## 4️⃣ Pseudocode — **Restore Soft-Deleted Todo**

```
START restoreTodo

READ todo ID from request parameters

FIND todo by ID where:
    - softDelete is true

UPDATE todo:
    - set softDelete = false
    - increment version by 1
    - return updated document

IF todo not found
    SEND 404 error
    STOP

LOG activity:
    - action = "restore"

SEND restored todo in response

END restoreTodo
```

---

## 5️⃣ Pseudocode — **Todo Statistics (Aggregation)**

```
START getTodoStats

SET current time

RUN aggregation pipeline:
    STEP 1: Select only non-deleted todos

    STEP 2: Run parallel aggregations:
        - Count todos grouped by status
        - Count overdue todos where:
            due date is before now
            status is not "done"

SEND aggregated statistics in response

END getTodoStats
```

---

## Big Mental Model 🧠

```
Read input
↓
Validate state (deleted / active)
↓
Update database atomically
↓
Increment version
↓
Log activity
↓
Send response
```

---

## Next-Level Improvement Ideas 💡

- 🔹 Use **MongoDB transactions**
    
    - Ensure Todo + Activity always stay in sync
        
- 🔹 Add **optimistic locking**
    
    - Reject update if version mismatch
        
- 🔹 Add **authorization**
    
    - Only owner can update/delete
        
- 🔹 Add **event-based logging**
    
    - Emit events instead of direct Activity writes
        
- 🔹 Add **materialized stats**
    
    - Cache stats for dashboards
        

If you want next:

- Controller **flowchart**
    
- **Interview explanation** of this controller
    
- **Exam-ready short answers**
    
- Convert this into **service-layer architecture**
    

Just say _continue_ 🚀

# src/models/todo.model.js
