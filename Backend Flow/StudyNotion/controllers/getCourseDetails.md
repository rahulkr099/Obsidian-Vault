## 🔹 GET COURSE DETAILS (PUBLIC)

### Function: `getCourseDetails(request, response)`

```
START getCourseDetails

TRY
    READ courseId from request body

    FETCH course by courseId
        POPULATE instructor
            POPULATE additionalDetails
        POPULATE category
        POPULATE ratingAndReviews
        POPULATE courseContent
            POPULATE subSection

    IF course not found
        RETURN response
            status = 400
            success = false
            message = "Course not found"
    END IF

    RETURN response
        status = 200
        success = true
        message = "Course details fetched successfully"
        data = course details

CATCH error
    LOG error
    RETURN response
        status = 500
        success = false
        error = error message
END TRY

END getCourseDetails
```

💡 **Improvements**

- Hide draft courses
    
- Remove sensitive instructor info
    