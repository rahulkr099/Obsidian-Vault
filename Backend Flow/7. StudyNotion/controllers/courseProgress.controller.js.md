Nice 👍  
This is a **clean and important feature** (progress tracking).  
Let’s convert it into **very detailed, slow, line-by-line pseudocode**, exactly like before.

I’ll keep words simple and logic crystal clear.

---

# 📁 courseProgressController.js — Detailed Pseudocode

[[Subsection.model.js]]
[[CourseProgress.model.js]]

---

## 🔹 UPDATE COURSE PROGRESS

### Function: `updateCourseProgress(request, response)`

```
START updateCourseProgress

    // Step 1: Read required data
    READ courseId from request body
    READ subsectionId from request body
    READ userId from request.user.id
```

---

### 🔸 Step 2: Validate Subsection

```
TRY
    FETCH subsection document using subsectionId

    IF subsection does not exist
        RETURN response
            status = 404
            success = false
            message = "Invalid subsection"
    END IF
```

📌 **Why this step?**  
Prevents marking progress for a video that does not exist.

---

### 🔸 Step 3: Fetch Course Progress for User

```
    FETCH CourseProgress document
        WHERE courseID = courseId
        AND userId = userId
```

---

### 🔸 Step 4: Validate Course Progress Existence

```
    IF courseProgress document does not exist
        RETURN response
            status = 404
            success = false
            message = "Course progress does not exist"
    END IF
```

📌 **Why this step?**  
Progress should only be updated for:

- enrolled users
    
- initialized progress records
    

---

### 🔸 Step 5: Prevent Duplicate Completion

```
    IF completedVideos array already contains subsectionId
        RETURN response
            status = 400
            success = false
            message = "Subsection already completed"
    END IF
```

📌 **Why this step?**  
Prevents:

- double counting progress
    
- incorrect completion percentage
    

---

### 🔸 Step 6: Update Progress

```
    ADD subsectionId to completedVideos array
```

---

### 🔸 Step 7: Save Progress

```
    SAVE updated CourseProgress document
```

---

### 🔸 Step 8: Send Success Response

```
    RETURN response
        status = 200
        success = true
        message = "Course progress updated"
```

---

### 🔸 Error Handling

```
CATCH any error
    LOG error

    RETURN response
        status = 500
        success = false
        message = "Internal server error"
END TRY
```

---

## 🔚 END FUNCTION

```
END updateCourseProgress
```

---

## 🚀 Improvement Ideas (Forward Thinking)

You’re already doing it right. Here’s how to make it **even better**:

### 1️⃣ Auto-create CourseProgress

Instead of returning 404:

```
IF courseProgress does not exist
    CREATE new CourseProgress document
```

### 2️⃣ Use `$addToSet`

Prevents duplicates automatically:

```
UPDATE CourseProgress
    ADD subsectionId using $addToSet
```

### 3️⃣ Verify Enrollment

Before updating progress:

```
CHECK if user is enrolled in course
```

### 4️⃣ Calculate Completion %

Store progress percentage for fast UI rendering.

---

## 🧠 Interview Explanation Tip

If asked:

> “How do you track course progress?”

You can confidently say:

- Each user has a CourseProgress document
    
- Completed videos are stored as subsection IDs
    
- Duplicate entries are prevented
    
- Progress is updated incrementally
    

---

If you want next:

- Convert this into **service layer**
    
- Add **course completion logic**
    
- Add **certificate trigger**
    
- Write **flowchart diagram**
    

Just tell me 👍