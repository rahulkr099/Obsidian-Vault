## 🔹 CREATE CATEGORY

### Function: `createCategory(request, response)`

```
START createCategory

TRY
    READ name and description from request body

    IF name is missing
        RETURN response
            status = 400
            success = false
            message = "All fields are required"
    END IF

    CREATE a new Category document
        category.name = name
        category.description = description

    SAVE category in database

    LOG saved category details (for debugging)

    RETURN response
        status = 200
        success = true
        message = "Category Created Successfully"

CATCH any error
    RETURN response
        status = 500
        success = false
        message = error message
END TRY

END createCategory
```

💡 **Improvement ideas**

- Check for duplicate category names
    
- Add slug field for SEO
    
- Normalize category name (lowercase)
    
