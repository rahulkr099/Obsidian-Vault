## 🔹 UPDATE SUB-SECTION

### Function: `updateSubSection(request, response)`

```
START updateSubSection

TRY
    // Step 1: Read input data
    READ sectionId from request body
    READ subSectionId from request body
    READ title from request body
    READ description from request body
```

---

### 🔸 Step 2: Fetch SubSection

```
    FETCH SubSection by subSectionId

    IF SubSection not found
        RETURN response
            status = 404
            success = false
            message = "SubSection not found"
    END IF
```

📌 **Why this step?**  
Cannot update something that doesn’t exist.

---

### 🔸 Step 3: Update Text Fields (If Provided)

```
    IF title is provided
        UPDATE subSection.title
    END IF

    IF description is provided
        UPDATE subSection.description
    END IF
```

📌 Partial updates are allowed.

---

### 🔸 Step 4: Update Video (Optional)

```
    IF request contains new video file
        UPLOAD new video to Cloudinary

        UPDATE:
            subSection.videoUrl = new secure_url
            subSection.timeDuration = new duration
    END IF
```

📌 **Why optional?**  
User may only update title or description.

---

### 🔸 Step 5: Save SubSection

```
    SAVE updated SubSection document
```

---

### 🔸 Step 6: Fetch Updated Section

```
    FETCH Section by sectionId
    POPULATE subSection
```

---

### 🔸 Step 7: Send Response

```
    RETURN response
        success = true
        message = "Section updated successfully"
        data = updated section
```

---

### 🔸 Error Handling

```
CATCH error
    LOG error

    RETURN response
        success = false
        message = "An error occurred while updating the section"
END TRY

END updateSubSection
```

💡 **Improvement ideas**

- Delete old video from Cloudinary
    
- Authorization check (instructor only)
    
- Track last updated time
    
