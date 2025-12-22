## 🔹 GET ENROLLED COURSES (WITH PROGRESS)

### Function: `getEnrolledCourses(request, response)`

```
START getEnrolledCourses

TRY
    // Step 1: Get user ID
    READ userId from request.user.id

    // Step 2: Fetch user with enrolled courses
    FETCH User by userId
        POPULATE courses
            POPULATE courseContent
                POPULATE subSection

    CONVERT userDetails to plain object

    // Step 3: Loop through courses
    FOR each course in user.courses
        SET totalDurationInSeconds = 0
        SET totalSubsections = 0

        FOR each section in course.courseContent
            ADD sum of subsection timeDuration to totalDurationInSeconds
            ADD subsection count to totalSubsections
        END FOR

        CONVERT totalDurationInSeconds to readable format
        SET course.totalDuration

        // Step 4: Fetch course progress
        FETCH CourseProgress
            WHERE courseID = course._id
            AND userId = userId

        SET completedCount = completedVideos length

        // Step 5: Calculate progress percentage
        IF totalSubsections is 0
            SET progressPercentage = 100
        ELSE
            CALCULATE (completedCount / totalSubsections) * 100
            ROUND to 2 decimal places
        END IF

        SET course.progressPercentage
    END FOR

    // Step 6: Return response
    RETURN response
        success = true
        data = list of enrolled courses with progress

CATCH error
    RETURN response
        success = false
        message = error message
END TRY

END getEnrolledCourses
```

💡 **Improvement ideas**

- Store progress percentage in DB
    
- Cache computed duration
    
- Optimize nested loops
    
