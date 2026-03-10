## 🔹 CATEGORY PAGE DETAILS (Main Logic)

### Function: `categoryPageDetails(request, response)`

```
START categoryPageDetails

TRY
    READ categoryId from request body
    LOG categoryId for debugging

    // STEP 1: Fetch selected category with published courses
    FETCH category by categoryId
        POPULATE courses where status = "Published"
        POPULATE ratingAndReviews inside courses

    IF selectedCategory does not exist
        LOG "Category not found"
        RETURN response
            status = 404
            success = false
            message = "Category not found"
    END IF

    IF selectedCategory.courses list is empty
        LOG "No courses found for the selected category"
        RETURN response
            status = 404
            success = false
            message = "No courses found for the selected category"
    END IF

    // STEP 2: Fetch categories except selected one
    FETCH categories where _id is NOT equal to categoryId

    PICK one random category using getRandomInt()

    FETCH that random category
        POPULATE courses where status = "Published"

    STORE this as differentCategory

    // STEP 3: Fetch top-selling courses across all categories
    FETCH all categories
        POPULATE courses where status = "Published"
        POPULATE instructor inside each course

    EXTRACT all courses from all categories into a single list

    SORT courses list by sold count (descending)

    PICK top 10 courses from sorted list

    STORE this as mostSellingCourses

    // STEP 4: Send final response
    RETURN response
        status = 200
        success = true
        data:
            selectedCategory
            differentCategory
            mostSellingCourses

CATCH any error
    RETURN response
        status = 500
        success = false
        message = "Internal server error"
        error = error message
END TRY

END categoryPageDetails
```

💡 **Improvement ideas**

- Avoid random category if none exist
    
- Cache mostSellingCourses
    
- Move sorting logic to aggregation pipeline
    
