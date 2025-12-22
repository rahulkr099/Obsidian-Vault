## Pseudocode for **List Todos**
- List Todos with filters, search, pagination and sorting
```bash
START listTodos

1.READ query parameters:
    page, limit, status, tag, q, searchText, sortBy
	SET default values if not provided

2.CREATE base filter:(fetch only active items)
    softDelete = false

3.IF status is provided
    ADD status to filter

4.IF tag is provided
    SPLIT tags by comma
    FILTER todos that contain any of these tags

5.CREATE database 'query' using filters [search this line on net]

6.IF search text exists
	On 'query'
	   - APPLY text search on todos
	   - SORT results by search relevance

7.CONVERT sortBy string into sorting rules

8.On 'query'
	APPLY sorting('7')
    SKIP (page - 1) * limit (Pagination skip)
	LIMIT number of results (Pagination limit)

9. RUN query + parallel in parallel for performance
    execute todo query
    count total matching todos

10.SEND response:
    list of todos
    metadata (total, page, limit)

END listTodos
```

---

## Pseudocode for **parseSort Helper**
- Convert "priority,-dueDate" into { priority: 1, dueDate: -1 }
```bash
START parseSort

1.Split the input string by commas as rawFields

2.Trim spaces around each field name
    fields = EMPTY LIST
    FOR each item IN rawFields:
        trimmed = TRIM(item)
        ADD trimmed TO fields

3.Prepare output object
    result = EMPTY MAP

4.FOR each field IN fields:
	4(1)IF field IS EMPTY:
	        CONTINUE TO NEXT field

	4(2)IF field STARTS WITH "-":
		    // Example: "-dueDate" → key = "dueDate", value = -1
	        key = REMOVE FIRST CHARACTER OF field
	        result[key] = -1
        
	4(3)ELSE
	        // Normal ascending field
	        result[field] = +1

    RETURN result

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

---
