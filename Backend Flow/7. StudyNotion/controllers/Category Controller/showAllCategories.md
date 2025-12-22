## 🔹 SHOW ALL CATEGORIES

### Function: `showAllCategories(request, response)`

```
START showAllCategories

TRY
    LOG "INSIDE SHOW ALL CATEGORIES" (debugging)

    FETCH all documents from Category collection

    RETURN response
        status = 200
        success = true
        data = list of all categories

CATCH any error
    RETURN response
        status = 500
        success = false
        message = error message
END TRY

END showAllCategories
```

💡 **Improvement ideas**

- Add pagination
    
- Add caching (Redis)
    
- Return only required fields
    