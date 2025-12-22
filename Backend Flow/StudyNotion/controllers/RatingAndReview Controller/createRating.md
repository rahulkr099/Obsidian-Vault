## 🔹 CREATE RATING & REVIEW

### Function: `createRating(request, response)`

```
START createRating

TRY
    // Step 1: Get logged-in user ID
    READ userId from request.user.id

    // Step 2: Read input data
    READ rating from request body
    READ review from request body
    READ courseId from request body
```

---

### 🔸 Step 3: Check if user is enrolled in the course

```
    FETCH course
        WHERE _id = courseId
        AND studentsEnrolled contains userId

    IF course not found
        RETURN response
            status = 404
            success = false
            message = "Student is not enrolled in the course"
    END IF
```

📌 **Why this step?**  
Only enrolled students are allowed to review a course.

---

### 🔸 Step 4: Prevent duplicate reviews

```
    FETCH RatingAndReview
        WHERE user = userId
        AND course = courseId

    IF review already exists
        RETURN response
            status = 403
            success = false
            message = "Course is already reviewed by the user"
    END IF
```

📌 **Why this step?**  
Prevents spam and fake multiple ratings from one user.

---

### 🔸 Step 5: Create rating & review

```
    CREATE RatingAndReview document
        rating = rating
        review = review
        course = courseId
        user = userId
```

---

### 🔸 Step 6: Attach rating to course

```
    UPDATE Course
        WHERE _id = courseId
        PUSH ratingReviewId into ratingAndReviews array
```

---

### 🔸 Step 7: Send success response

```
    RETURN response
        status = 200
        success = true
        message = "Rating and Review created successfully"
        data = ratingReview
```

---

### 🔸 Error Handling

```
CATCH error
    RETURN response
        status = 500
        success = false
        message = error message
END TRY

END createRating
```

💡 **Improvement ideas**

- Validate rating range (1–5)
    
- Allow review edit/update
    
- Add moderation flag
    

---
