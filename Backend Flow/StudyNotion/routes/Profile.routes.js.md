## 📌 2. `Profile.js` – User Profile Management

```
START Profile Module

DEFINE Profile schema
    userId
    bio
    gender
    dateOfBirth
    contactNumber
    avatar

FUNCTION createOrUpdateProfile(userId, profileData)
    CHECK if profile exists
    IF exists
        UPDATE profile
    ELSE
        CREATE new profile
    ENDIF
    RETURN updated profile
END

FUNCTION getProfile(userId)
    FETCH profile using userId
    RETURN profile details
END

END Profile Module
```
