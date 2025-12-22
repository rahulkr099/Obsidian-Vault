## 📌 3. `Course.js` – Courses Handling
[[Course.controller.js]]
```
START Course Module

DEFINE Course schema
    title
    description
    price
    instructor
    studentsEnrolled
    createdAt

FUNCTION createCourse(courseData)
    VALIDATE data
    SAVE course in database
    RETURN course
END

FUNCTION getAllCourses()
    FETCH all courses
    RETURN course list
END

FUNCTION getCourseById(courseId)
    FETCH course details
    RETURN course
END

FUNCTION enrollUser(courseId, userId)
    ADD user to course enrollment
    UPDATE course record
END

END Course Module
```
