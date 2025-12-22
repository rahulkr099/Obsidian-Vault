## 🔹 SHOW ALL COURSES (PUBLISHED)

### Function: `showAllCourses(request, response)`

```
START showAllCourses

TRY
    FETCH all courses
        WHERE status = "Published"
        SELECT fields:
            courseName
            price
            thumbnail
            instructor
            ratingAndReviews
            studentsEnrolled

    POPULATE instructor details

    RETURN response
        status = 200
        success = true
        message = "Data for all courses fetched successfully"
        data = courses list

CATCH error
    LOG error
    RETURN response
        status = 500
        success = false
        message = "Cannot fetch course data"
END TRY

END showAllCourses
```

💡 **Improvements**

- Pagination
    
- Sorting by rating / popularity
    
- Cache results
    
