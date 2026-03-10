## 🔹 GET FULL COURSE DETAILS (ENROLLED USER)

### Function: `getFullCourseDetails(request, response)`

```
START getFullCourseDetails

TRY
    READ courseId from request body
    READ userId from request.user.id

    FETCH course with full population

    FETCH course progress for user

    IF course not found
        RETURN response
            status = 400
            success = false
            message = "Course not found"
    END IF

    SET totalDurationInSeconds = 0

    FOR each section in courseContent
        FOR each subSection in section
            CONVERT timeDuration to integer
            ADD to totalDurationInSeconds
        END FOR
    END FOR

    CONVERT totalDurationInSeconds to readable format

    RETURN response
        success = true
        data:
            courseDetails
            totalDuration
            completedVideos (or empty array)

CATCH error
    RETURN response
        status = 500
        success = false
        message = error message
END TRY

END getFullCourseDetails
```

💡 **Improvements**

- Restrict access to enrolled users only
    
- Cache duration
    
