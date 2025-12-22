## 3️⃣ Pseudocode — **Soft Delete Todo**
- Soft delete (not removing document physically)
```bash
START softDeleteTodo

1.READ todo ID from request parameters

2.FIND todo by ID and UPDATE where:
	3(1)FIND todo
		- id
	    - not soft deleted

	3(2)UPDATE todo:
	    - set softDelete = true
	    - increment version by 1
	      
	3(3)RETURN updated document

4.IF todo not found
    SEND 404 error
    STOP

5.CREATE LOG activity:
	store todo Id
    action = "delete"
    store payload as NULL

6.SEND updated todo in response

END softDeleteTodo
```
