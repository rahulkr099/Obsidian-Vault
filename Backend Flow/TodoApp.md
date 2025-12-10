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
1. Require files and libraries
2. Initialize express app
3. Use middleware
4. Define routes
5. Health Check Route
6. Handle undefined route
7. Centralised error handling
8. Exporting this file for starting the server
```
# server.js
```
1. Require files and libraries
2. Load environment variables
3. try-catch
4. Connecting to a database
5. Start the server
6. Catch the error
7. Start()
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

