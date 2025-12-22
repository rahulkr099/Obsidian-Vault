## 🔹 GET ALL USER DETAILS

### Function: `getAllUserDetails(request, response)`

```
START getAllUserDetails

TRY
    // Step 1: Get user ID
    READ userId from request.user.id

    // Step 2: Fetch user with profile
    FETCH User by userId
        POPULATE additionalDetails

    // Step 3: Return response
    RETURN response
        success = true
        message = "User data fetched successfully"
        data = user details

CATCH error
    RETURN response
        success = false
        message = error message
END TRY

END getAllUserDetails
```

💡 **Improvement ideas**

- Hide sensitive fields
    
- Add caching
    
