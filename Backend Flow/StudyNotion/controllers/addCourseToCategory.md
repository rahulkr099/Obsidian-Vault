## 🔹 ADD COURSE TO CATEGORY

### Function: `addCourseToCategory(request, response)`

```
START addCourseToCategory

READ courseId and categoryId from request body

TRY
    FETCH category using categoryId

    IF category does not exist
        RETURN response
            status = 404
            success = false
            message = "Category not found"
    END IF

    FETCH course using courseId

    IF course does not exist
        RETURN response
            status = 404
            success = false
            message = "Course not found"
    END IF

    CHECK if courseId already exists in category.courses array

    IF course already exists
        RETURN response
            status = 200
            success = true
            message = "Course already exists in the category"
    END IF

    ADD courseId to category.courses array

    SAVE updated category document

    RETURN response
        status = 200
        success = true
        message = "Course added to category successfully"

CATCH any error
    RETURN response
        status = 500
        success = false
        message = "Internal server error"
        error = error message
END TRY

END addCourseToCategory
```

💡 **Improvement ideas**

- Use `$addToSet` instead of manual check
    
- Validate course publish status
    
- Add transaction for consistency
    
## 🚀 Big-Picture Growth Ideas (Next Level)

You’re already writing **industry-grade code**. To push it further:

- Move logic to **CategoryService**
    
- Use **MongoDB aggregation** for top-selling courses
    
- Add **Redis caching** for category pages
    
- Add **indexes** on `sold`, `status`, `categoryId`
    

If you want next:

- I can convert this into **service + controller architecture**
    
- Or draw **request → DB → response flow**
    
- Or make **interview-ready explanations**
    

Just tell me 👍