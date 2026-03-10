## 🔹 ENROLL STUDENTS AFTER PAYMENT

### Function: `enrollStudents(courses, userId, response)`

```
START enrollStudents

    IF courses OR userId is missing
        RETURN response
            success = false
            message = "Please provide course or userId"
    END IF
```

---

### 🔸 Step 1: Loop Through Courses

```
    FOR each courseId in courses
        TRY
            // Add student to course
            UPDATE Course
                PUSH userId into studentsEnrolled

            IF course not found
                RETURN response
                    success = false
                    message = "Course not found"
            END IF
```

---

### 🔸 Step 2: Create Course Progress

```
            CREATE CourseProgress document
                courseID = courseId
                userId = userId
                completedVideos = empty array
```

---

### 🔸 Step 3: Add Course to User Profile

```
            UPDATE User document
                PUSH courseId into user.courses
                PUSH courseProgressId into user.courseProgress
```

---

### 🔸 Step 4: Send Enrollment Email

```
            SEND email to student
                subject = "Successfully Enrolled"
                body = course enrollment email template
```

---

### 🔸 Error Handling

```
        CATCH error
            LOG error
            RETURN response
                success = false
                message = error.message
        END TRY
    END FOR

END enrollStudents
```

📌 **Why this step?**

- Links course ↔ user ↔ progress
    
- Initializes learning tracking
    
- Sends confirmation email
    
