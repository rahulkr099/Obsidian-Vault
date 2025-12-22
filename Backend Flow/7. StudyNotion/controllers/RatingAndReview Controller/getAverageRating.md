## 🔹 GET AVERAGE RATING OF A COURSE

### Function: `getAverageRating(request, response)`

```
START getAverageRating

TRY
    // Step 1: Read courseId
    READ courseId from request body
```

---

### 🔸 Step 2: Calculate average rating using aggregation

```
    PERFORM aggregation on RatingAndReview collection

    PIPELINE:
        MATCH documents where course = courseId
        GROUP all matched documents
            CALCULATE average of rating field
```

---

### 🔸 Step 3: Handle aggregation result

```
    IF result contains data
        RETURN response
            success = true
            averageRating = calculated average
    ELSE
        RETURN response
            success = true
            message = "Average rating is 0, no ratings yet"
            averageRating = 0
    END IF
```

---

### 🔸 Error Handling

```
CATCH error
    RETURN response
        success = false
        message = error message
END TRY

END getAverageRating
```

💡 **Improvement ideas**

- Cache average rating in Course model
    
- Round rating to 1 decimal place
    
- Update average on new review
    
