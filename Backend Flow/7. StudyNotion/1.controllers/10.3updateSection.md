## 🔹 UPDATE SECTION

### Function: `updateSection(request, response)`

```
START updateSection

TRY
    // Step 1: Read input data
    READ sectionName from request body
    READ sectionId from request body
    READ courseId from request body
```

---

### 🔸 Step 2: Update Section Name

```
    UPDATE Section document
        WHERE _id = sectionId
        SET sectionName = new sectionName
        RETURN updated section
```

📌 Only section name changes here.

---

### 🔸 Step 3: Fetch Updated Course Structure

```
    FETCH Course by courseId

    POPULATE courseContent
        POPULATE subSection inside each section
```

📌 **Why this step?**  
Frontend needs updated course structure after section rename.

---

### 🔸 Step 4: Send Response

```
    RETURN response
        status = 200
        success = true
        message = updated section
        data = updated course
```

---

### 🔸 Error Handling

```
CATCH error
    LOG error
    RETURN response
        status = 500
        success = false
        message = "Internal server error"
END TRY

END updateSection
```

💡 **Improvement ideas**

- Validate section belongs to course
    
- Validate instructor authorization
    
