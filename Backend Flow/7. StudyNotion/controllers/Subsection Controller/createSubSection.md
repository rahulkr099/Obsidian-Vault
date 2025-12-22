## 🔹 CREATE SUB-SECTION (Add Lecture / Video)

### Function: `createSubSection(request, response)`

```
START createSubSection

TRY
    // Step 1: Read input data
    READ sectionId from request body
    READ title from request body
    READ description from request body
    READ video file from request.files
```

---

### 🔸 Step 2: Validate Required Fields

```
    IF sectionId is missing
       OR title is missing
       OR description is missing
       OR video file is missing
    THEN
        RETURN response
            status = 404
            success = false
            message = "All fields are required"
    END IF
```

📌 **Why this step?**  
A sub-section must:

- belong to a section
    
- have a title
    
- have description
    
- contain a video
    

---

### 🔸 Step 3: Upload Video to Cloudinary

```
    UPLOAD video file to Cloudinary
        USING uploadImageToCloudinary()

    RECEIVE uploadDetails
        uploadDetails.secure_url → video URL
        uploadDetails.duration   → video length
```

📌 **Why Cloudinary?**

- Stores video
    
- Returns URL
    
- Gives duration automatically
    

---

### 🔸 Step 4: Create SubSection Document

```
    CREATE SubSection document
        title = title
        description = description
        videoUrl = uploadDetails.secure_url
        timeDuration = uploadDetails.duration
```

📌 At this point:

- SubSection exists independently
    
- Not yet linked to section
    

---

### 🔸 Step 5: Attach SubSection to Section

```
    UPDATE Section document
        WHERE _id = sectionId
        PUSH SubSection ID into subSection array
        RETURN updated Section
```

---

### 🔸 Step 6: Populate SubSections

```
    POPULATE subSection field of Section
```

📌 **Why populate?**  
Frontend needs full updated section immediately.

---

### 🔸 Step 7: Send Success Response

```
    RETURN response
        status = 200
        success = true
        data = updated section
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
        error = error.message
END TRY

END createSubSection
```

💡 **Improvement ideas**

- Validate video format & size
    
- Add lecture order number
    
- Transaction for safety
    
