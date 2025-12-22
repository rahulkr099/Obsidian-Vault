### 2️⃣ Get a Single Todo (not deleted)

```bash
START getTodo

1.READ todo ID from request parameters

2.SEARCH database for todo:
    match ID
    softDelete must be false

3.IF todo is NOT found
    SEND response:
        - status = 404
        - error = "Not found"
    STOP

4.SEND response
    return todo data

END getTodo
```

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
        


---

