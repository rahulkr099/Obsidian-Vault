## 1️⃣ Pseudocode — **Update Todo (Partial Update)**
- Update fields partially
- Version increments every update
```bash
START updateTodo

1.READ todo ID from request parameters
2.READ update data from request body as payload

3.FIND todo by ID to UPDATE where:
	3(1)FIND todo:
		    - id
			- not soft deleted
	3(2)UPDATE todo:
		    - set provided fields
		    - increment version by 1
	3(3)RETURN updated document

4.IF todo not found
    SEND 404 
    error "Not Found"
    STOP - RETURN 

5.CREATE LOG activity:
	- store todo ID
    - action = "update"
    - store payload

6.SEND updated todo in response

END updateTodo
```
