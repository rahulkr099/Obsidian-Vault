## 🔹 CREATE SECTION

### Function: `createSection(request, response)`

```
START createSection

TRY
    // Step 1: Read input data
    READ sectionName from request body
    READ courseId from request body
```

---

### 🔸 Step 2: Validate Input

```
    IF sectionName is missing OR courseId is missing
        RETURN response
            status = 400
            success = false
            message = "Missing required properties"
    END IF
```

📌 **Why this step?**  
A section must belong to a course and must have a name.

---

### 🔸 Step 3: Create Section

```
    CREATE new Section document
        sectionName = provided sectionName
```

📌 At this stage:

- Section exists independently
    
- Not yet linked to course
    

---

### 🔸 Step 4: Attach Section to Course

```
    UPDATE Course document
        WHERE _id = courseId
        PUSH newSection._id into courseContent array
        RETURN updated document
```

---

### 🔸 Step 5: Populate Course Content

```
    POPULATE courseContent
        POPULATE subSection inside each section
```

📌 **Why populate?**  
Frontend immediately receives full updated course structure.

---

### 🔸 Step 6: Send Success Response

```
    RETURN response
        status = 200
        success = true
        message = "Section created successfully"
        data = updated course
```

---

### 🔸 Error Handling

```
CATCH error
    RETURN response
        status = 500
        success = false
        message = "Internal server error"
        error = error.message
END TRY

END createSection
```

💡 **Improvement ideas**

- Validate instructor ownership
    
- Prevent duplicate section names
    
- Use transaction for safety
    
