## 🔹 UPDATE DISPLAY PICTURE

### Function: `updateDisplayPicture(request, response)`

```
START updateDisplayPicture

TRY
    // Step 1: Read image file
    READ displayPicture from request.files

    // Step 2: Read user ID
    READ userId from request.user.id

    // Step 3: Upload image to Cloudinary
    UPLOAD image
        with width = 1000
        with height = 1000

    GET secure image URL

    // Step 4: Update user image
    UPDATE User
        SET image = uploaded image URL

    // Step 5: Return success response
    RETURN response
        success = true
        message = "Image updated successfully"
        data = updated user

CATCH error
    RETURN response
        success = false
        message = error message
END TRY

END updateDisplayPicture
```

💡 **Improvement ideas**

- Validate image type
    
- Limit file size
    
- Delete old image from Cloudinary
    