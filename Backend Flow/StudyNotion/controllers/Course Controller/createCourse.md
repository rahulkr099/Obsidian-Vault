## 🔹 CREATE COURSE

### Function: `createCourse(request, response)`

```
START createCourse

TRY
    // Step 1: Get instructor ID
    READ userId from request.user.id

    // Step 2: Read all fields from request body
    READ courseName
    READ courseDescription
    READ whatYouWillLearn
    READ price
    READ tag (stringified array)
    READ category
    READ status
    READ instructions (stringified array)

    // Step 3: Read thumbnail image
    READ thumbnailImage from request.files

    // Step 4: Convert stringified arrays to real arrays
    PARSE tag into array
    PARSE instructions into array

    // Step 5: Validate required fields
    IF any of the following is missing:
        courseName
        courseDescription
        whatYouWillLearn
        price
        tag array is empty
        thumbnailImage
        category
        instructions array is empty
    THEN
        RETURN response
            status = 400
            success = false
            message = "All Fields are Mandatory"
    END IF

    // Step 6: Set default course status
    IF status is missing OR undefined
        SET status = "Draft"
    END IF

    // Step 7: Verify instructor
    FETCH user by userId
    CHECK accountType is Instructor

    IF instructor not found
        RETURN response
            status = 404
            success = false
            message = "Instructor Details Not Found"
    END IF

    // Step 8: Verify category
    FETCH category by category ID

    IF category not found
        RETURN response
            status = 404
            success = false
            message = "Category Details Not Found"
    END IF

    // Step 9: Upload thumbnail to Cloudinary
    UPLOAD thumbnail image
    GET secure URL

    // Step 10: Create new course
    CREATE Course document with:
        courseName
        courseDescription
        instructor ID
        whatYouWillLearn
        price
        tags
        category ID
        thumbnail URL
        status
        instructions

    // Step 11: Add course to instructor profile
    UPDATE User document
        PUSH course ID into instructor.courses

    // Step 12: Add course to category
    UPDATE Category document
        PUSH course ID into category.courses

    // Step 13: Send success response
    RETURN response
        status = 200
        success = true
        message = "Course Created Successfully"
        data = newly created course

CATCH error
    LOG error
    RETURN response
        status = 500
        success = false
        message = "Failed to create course"
END TRY

END createCourse
```

💡 **Improvements**

- Use MongoDB transaction
    
- Validate price > 0
    
- Slug for courseName
    

---