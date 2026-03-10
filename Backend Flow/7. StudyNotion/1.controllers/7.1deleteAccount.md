## 🔹 DELETE ACCOUNT

### Function: `deleteAccount(request, response)`

```
START deleteAccount

TRY
    // Step 1: Get user ID
    READ userId from request.user.id

    // Step 2: Fetch user
    FETCH User by userId

    IF user does not exist
        RETURN response
            success = false
            message = "User not found"
    END IF

    // Step 3: Delete associated profile
    DELETE Profile using user.additionalDetails ID

    // Step 4: Remove user from enrolled courses
    FOR each courseId in user.courses
        UPDATE Course
            REMOVE userId from studentsEnrolled
    END FOR

    // Step 5: Delete course progress records
    DELETE all CourseProgress documents
        WHERE userId = userId

    // Step 6: Delete user account
    DELETE User by userId

    // Step 7: Send success response
    RETURN response
        success = true
        message = "User deleted successfully"

CATCH error
    LOG error
    RETURN response
        success = false
        message = "User cannot be deleted successfully"
END TRY

END deleteAccount
```

💡 **Improvement ideas**

- Use MongoDB transactions
    
- Soft delete instead of hard delete
    
- Email confirmation before delete
    
