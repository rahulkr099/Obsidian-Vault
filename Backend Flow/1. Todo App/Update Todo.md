## 1️⃣ Pseudocode — **Update Todo (Partial Update)**
- Update fields partially
- Version increments every update
```bash
START updateTodo

1.READ todo ID from request parameters
2.Create update object:
	- status = 'done'
	- completedAt = current timestamp

3.FIND todo by ID to UPDATE where:
	3(1)FIND todo:
		    - match id
			- not soft deleted
	3(2)UPDATE todo:
		    - set fields from update object
		    - increment version by 1
	3(3)RETURN updated document

4.IF todo not found
    SEND 404 
    error "Not Found"
    STOP - RETURN 

5.CREATE LOG activity:
	- store todo ID
    - action = "completed"
    - store update payload

6.SEND updated todo in response

END updateTodo
```
