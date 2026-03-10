## 🔹 GET INSTRUCTOR COURSES

### Function: `getInstructorCourses(request, response)`

```
START getInstructorCourses

TRY
    READ instructorId from request.user.id

    FETCH all courses
        WHERE instructor = instructorId
        SORT by createdAt descending

    RETURN response
        success = true
        data = instructor courses

CATCH error
    LOG error
    RETURN response
        success = false
        message = "Failed to retrieve instructor courses"
END TRY

END getInstructorCourses
```
