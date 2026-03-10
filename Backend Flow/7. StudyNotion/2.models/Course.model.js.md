## 📌 5. `Course.js` – Courses

```
START Course Module

DEFINE Course schema
    title
    description
    instructor
    price
    category
    sections
    studentsEnrolled
    ratingAndReviews

FUNCTION createCourse(data)
    VALIDATE instructor role
    SAVE course
END

FUNCTION getCourseDetails(courseId)
    RETURN course info with sections
END

FUNCTION enrollUser(courseId, userId)
    ADD user to studentsEnrolled
    ADD course to user's courses
END

END Course Module
```
