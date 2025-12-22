## 4️⃣ Pseudocode — **Restore Soft-Deleted Todo**

```bash
START restoreTodo

1.READ todo ID from request parameters

2.FIND todo by ID and UPDATE where:
	2(1)FIND todo
		- id
	    - softDelete is true

	2(2)UPDATE todo:
	    - set softDelete = false
	    - increment version by 1
	      
2(3)RETURN updated document

3.IF todo not found
    SEND 404 
    error 'Not found or not deleted'
    STOP

4.CREATE LOG activity:
	- store todo id
    - action = "restore"
    - store payload as NULL

5.SEND restored todo in response

END restoreTodo
```
