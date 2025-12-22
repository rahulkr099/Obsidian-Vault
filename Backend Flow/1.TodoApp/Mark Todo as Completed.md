## 2️⃣ Pseudocode — **Mark Todo as Completed**

```bash
START completeTodo

1.READ todo ID from request parameters

2.CREATE update object:
	add status
	capture completion timestamp

3.FIND todo by ID and UPDATE where:
	3(1)FIND todo
		- id
		- not soft deleted

	3(2)UPDATE todo
	    - set update object
	    - increment version by 1
	3(3)RETURN updated document

4.IF todo not found
    SEND 404 error
    STOP - return

5.CREATE LOG activity:
	- store todo id
    - action = "complete"
    - store update data

6.SEND updated todo in response

END completeTodo
```
