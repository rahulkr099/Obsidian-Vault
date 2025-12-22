### 1️⃣ Create Todo

```bash
START createTodo

1.READ request body as payload

2.SAVE payload into database as new todo

3.LOG activity:
	store todo ID
    action = "create"
    store payload

4.SEND response:
    status = 201 (created)
    return created todo

END createTodo
```
