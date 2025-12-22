## 🔹 EDIT COURSE

### Function: `editCourse(request, response)`

```
START editCourse

TRY
    READ courseId from request body
    READ updated fields from request body

    FETCH course by courseId

    IF course not found
        RETURN response
            status = 404
            message = "Course not found"
    END IF

    // Handle thumbnail update
    IF thumbnailImage exists in request.files
        UPLOAD new thumbnail to Cloudinary
        UPDATE course.thumbnail
    END IF

    // Update provided fields only
    FOR each key in updated fields
        IF key is "tag" OR "instructions"
            PARSE value as JSON
            UPDATE course[key]
        ELSE
            UPDATE course[key]
        END IF
    END FOR

    SAVE course

    FETCH updated course with populated relations

    RETURN response
        success = true
        message = "Course updated successfully"
        data = updated course

CATCH error
    LOG error
    RETURN response
        status = 500
        success = false
        message = "Internal server error"
END TRY

END editCourse
```

💡 **Improvements**

- Prevent editing published course
    
- Validate ownership
    
