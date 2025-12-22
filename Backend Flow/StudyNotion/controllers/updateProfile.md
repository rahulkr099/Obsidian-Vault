## 🔹 UPDATE PROFILE

### Function: `updateProfile(request, response)`

```
START updateProfile

TRY
    // Step 1: Read profile fields from request body
    READ firstName (default empty)
    READ lastName (default empty)
    READ dateOfBirth (default empty)
    READ about (default empty)
    READ contactNumber (default empty)
    READ gender (default empty)

    // Step 2: Get logged-in user ID
    READ userId from request.user.id

    // Step 3: Fetch user details
    FETCH User by userId

    // Step 4: Fetch associated Profile using user.additionalDetails
    FETCH Profile by profileId

    // Step 5: Update user basic info
    UPDATE User
        SET firstName
        SET lastName
    SAVE user

    // Step 6: Update profile fields
    SET profile.dateOfBirth
    SET profile.about
    SET profile.contactNumber
    SET profile.gender

    // Step 7: Save profile
    SAVE profile

    // Step 8: Fetch updated user with populated profile
    FETCH User by userId
        POPULATE additionalDetails

    // Step 9: Send success response
    RETURN response
        success = true
        message = "Profile updated successfully"
        data = updated user details

CATCH error
    LOG error
    RETURN response
        success = false
        error = error message
END TRY

END updateProfile
```

💡 **Improvement ideas**

- Validate phone number
    
- Prevent empty overwrites
    
- Add profile completion %
    
