## 7. Driver Updates Location (Real-Time ⭐)

```
WHEN POST /driver/location

  Update driver location in database

  IF driver has an active ride
    Emit socket event to rider:
      "driver:location"
```

⭐ **Why interviewers like this**  
Shows real-time system thinking.