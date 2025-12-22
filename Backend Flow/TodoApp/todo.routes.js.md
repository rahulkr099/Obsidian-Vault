```text
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
[[todo.controller.js]]
[[validate.js]]

# src/routes/todo.routes.js
```bash
Purpose: CRUD routes of todo

1.Router Instance Initializaton
	IMPORT Express framework
	CREATE a router instance of express

2.Require controller and middlewares
	IMPORT todo controller
	IMPORT request validation functions

====== CRUD routes =======
3.DEFINE route: POST "/"
    VALIDATE create request [[validate.js]]
    CALL controller to create a todo [[createTodo]]

4.DEFINE route: GET "/"
    CALL controller to list all todos [[List Todo]]

5.DEFINE route: GET "/stats"
    CALL controller to return todo statistics [[Todo Statistics]]

6.DEFINE route: GET "/:id"
    EXTRACT todo id from request 
    CALL controller to fetch single todo [[Get a Single Todo]]

7.DEFINE route: PATCH "/:id"
    VALIDATE update request [[validate.js]]
    CALL controller to update todo [[Update Todo]]

8.DEFINE route: PATCH "/:id/complete"
    MARK the given todo as completed [[Mark Todo as Completed]]

9.DEFINE route: DELETE "/:id"
    SOFT DELETE the given todo [[Soft delete Todo]]

10.DEFINE route: POST "/:id/restore"
    RESTORE a previously deleted todo [[Restore Soft deleted Todo]]

EXPORT router
```

```
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
