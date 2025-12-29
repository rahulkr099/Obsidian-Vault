Alright Rahul — here is a **premium, industry-style machine coding round mock question** focused on **setInterval, clearInterval, timers, stopwatch & countdown**, with:

✔ Edge cases  
✔ Failure scenarios  
✔ Acceptance criteria  
✔ Test cases  
✔ Bonus features

This is EXACTLY the type companies use to test **JS fundamentals**, timing functions, clean state handling, and UI updates.

Let’s do it properly — simple words, clear thinking, strong learning.

---

# 🚀 **🔥 MACHINE CODING ROUND – Stopwatch + Countdown Timer**

## ⏱ Duration: 45 minutes

## 🧪 Difficulty: Medium

## 🧰 Tech: HTML + CSS + JavaScript (NO frameworks)

---

# 📝 **📌 Problem Statement**

Build **two time-based components**:

1. **Stopwatch**
    
2. **Countdown Timer (user enters time)**
    

Both should use **setInterval() and clearInterval() properly**, with clean state management.

Extra features:

- Lap recording (for Stopwatch)
    
- Sound alert when countdown finishes
    

---

# 🧩 **📋 Functional Requirements**

---

## ⭐ 1️⃣ Stopwatch

### Must Have:

- **Start** button → begin counting
    
- **Pause** button → stop counting but retain time
    
- **Reset** button → set time back to `00:00:00`
    
- Time format:
    
    ```
    mm:ss:ms
    ```
    
    Example → `05:23:450`
    

### Stopwatch Rules:

- If running, Start button should not create multiple intervals
    
- Reset should also clear the interval
    

---

## ⭐ 2️⃣ Countdown Timer

### Inputs:

- Minutes
    
- Seconds
    

### Must Have:

- Start countdown
    
- Pause countdown
    
- Reset countdown
    
- Display time updating every second
    

### End Behavior:

- When timer hits zero →
    
    - Stop automatically
        
    - Show “Time’s Up!”
        
    - Play a sound (extra)
        

---

## ⭐ 3️⃣ Lap Feature (Extra)

For Stopwatch:

- Click LAP → store current running time
    
- Show laps in a list
    
- Lap should work only when stopwatch is running
    

---

# ⚠️ **📌 Edge Cases (Very important!)**

### Stopwatch Edge Cases:

- User clicks Start multiple times → must NOT create multiple intervals
    
- Reset while paused → ok
    
- Reset while running → must clear interval AND reset time
    
- Start → Pause → Start again → should continue properly
    
- Interval drift (ms accuracy) → acceptable at beginner level
    
- Pressing Lap when paused → ignore
    

### Countdown Edge Cases:

- User enters negative numbers → treat as invalid
    
- User enters empty fields → treat as 0
    
- Seconds >= 60 → normalize (optional)
    
- Countdown hits exactly 0 → stop clean
    
- Start multiple times → must not speed up
    
- Reset while running → stop interval and set back to original
    

### UI / User Input Edge Cases:

- Non-numeric input → reject or convert to number
    
- Very large numbers (e.g. 999 minutes) → should still work
    
- Countdown reaches 0 in the middle of pause → ignore
    

### Sound:

- If audio fails to load → no crash
    

---

# ❌ **📌 Failure Scenarios (Show deep thinking)**

- Multiple intervals created due to bad Start logic
    
- Interval not cleared → memory leak
    
- Timer UI continues but logic stops
    
- Lap list duplicates because of repeated event binding
    
- Countdown ends but UI doesn’t show “Time’s Up!”
    
- NaN appears because input not validated
    
- User enters decimals → floor or reject
    
- User deletes input while running timer → freeze
    

---

# 🎯 **📌 Acceptance Criteria (Pass/Fail)**

### UI:

- Clean time display
    
- Visible buttons
    
- Laps listed clearly
    
- Countdown input simple
    

### Behavior:

- Timers accurate enough (~1ms drift okay)
    
- Interval always cleared on pause/reset
    
- Buttons behave correctly in all states
    
- No flashing/flickering
    
- Countdown stops exactly at 0
    
- “Time’s up” indicator visible
    
- Lap timestamps correct
    

### Code:

- Functions separated:
    
    - startStopwatch()
        
    - pauseStopwatch()
        
    - resetStopwatch()
        
    - startCountdown()
        
    - pauseCountdown()
        
    - resetCountdown()
        
    - updateStopwatchUI()
        
    - updateCountdownUI()
        
- No repeated logic
    
- Clean variable names
    
- No global event leaks
    
- No inline event handlers
    
- No console errors
    

---

# 🧪 **📌 Test Cases**

|Action|Expected Result|
|---|---|
|Start stopwatch|Time increases|
|Pause stopwatch|Time stops increasing|
|Reset stopwatch|00:00:00|
|Start → Pause → Start|Continues correctly|
|Press Start twice|No speed doubling|
|Lap while running|Correct lap recorded|
|Lap while paused|No lap added|
|Countdown: enter 1 min, start|Goes 01:00 → 00:59…|
|Countdown ends|Show “Time’s up!” + sound|
|Pause countdown|Stops decreasing|
|Reset countdown|Returns to input time|
|Enter negative or empty time|Treat as 0|
|Enter non-numeric time|Handle gracefully|
|Click Start multiple times|No extra intervals|
|Stop → Start → Reset|Always stable|

---

# 🌟 **📌 Bonus Points (Optional but boosts your interview score)**

### Stopwatch:

- Lap difference calculation (split timing)
    
- Highlight fastest/slowest lap
    

### Countdown:

- Animated progress bar
    
- Save input in localStorage
    
- “Add 10 seconds” button
    
- Choose alarm sound
    

### General:

- Combine both components into reusable classes
    
- Make UI responsive
    
- Add dark/light mode
    

---

# 🎤 **📌 Interviewer Evaluation Guide**

They look for:

### Logic & State:

- Clean interval management
    
- No double intervals
    
- Correct time formatting
    
- Accurate countdown stopping
    

### UI:

- Smooth time updates
    
- Laps readable
    
- Disabled inputs during countdown (optional)
    

### Code:

- Modular
    
- Commented
    
- Clear functions
    
- No duplication
    

### Behavior:

- Works in all edge cases
    
- Stable under fast clicking
    
- No crashes
    

---

Rahul — this is EXACTLY how machine coding timer problems are evaluated.

If you want:

👉 Start this mock round  
👉 Get full working solution  
👉 Get optimized version  
👉 Get React version  
👉 Get TypeScript class-based implementation

Just tell me!