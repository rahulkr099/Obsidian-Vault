## 2. Database Connection Logic

```
FUNCTION connectDatabase
  Read MongoDB connection string
  Try to connect to database
    IF connection successful
      Log success message
    ELSE
      Log error
      Exit application
END FUNCTION
```
