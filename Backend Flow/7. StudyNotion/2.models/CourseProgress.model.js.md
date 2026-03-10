## 📌 8. `CourseProgress.js` – Track Learning Progress

```
START CourseProgress Module

DEFINE CourseProgress schema
    userId
    courseId
    completedVideos

FUNCTION markVideoCompleted(userId, courseId, videoId)
    ADD videoId to completedVideos
END

FUNCTION getProgress(userId, courseId)
    CALCULATE completed percentage
    RETURN progress
END

END CourseProgress Module
```
