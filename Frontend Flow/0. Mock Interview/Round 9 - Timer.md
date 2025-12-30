Alright Rahul, here comes a neat, interview-ready **mock machine coding question** for a **Timer Component**.  
This round tests timing logic, clean state updates, and a bit of formatting — simple but very telling in interviews.

---

# ✅ **Mock Interview Question — Timer (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 30 minutes

### **🎯 Goal:** Build a **Start / Pause / Reset** timer displaying time in **mm:ss** format.

---

# **📝 Problem Statement**

Create a **Timer Component** that:

- Counts time in minutes and seconds
    
- Can start, pause, and reset
    
- Updates the displayed time every second
    

The timer should begin at **00:00** and increase upward.

---

# **💡 Functional Requirements**

### **1️⃣ Start**

- Clicking **Start** begins the timer from the current time.
    
- Should update every 1000ms.
    
- If already running and Start is clicked again → nothing should change.
    

### **2️⃣ Pause**

- Clicking **Pause** stops the timer.
    
- Clicking **Start** again resumes from where it stopped.
    

### **3️⃣ Reset**

- Clicking **Reset**:
    
    - Stops the timer
        
    - Sets time to **00:00**
        
    - Clears all internal intervals
        

### **4️⃣ Display Format**

- Must always show **mm:ss** format.
    
    - 0 → `00:00`
        
    - 9 seconds → `00:09`
        
    - 71 seconds → `01:11`
        

Use zero-padding everywhere.

### **5️⃣ Buttons**

- Start
    
- Pause
    
- Reset
    
- Should look usable and responsive.
    

---

# **🧪 Edge Cases to Handle**

- Multiple Start clicks → should not create multiple intervals running in background.
    
- Fast clicking Start/Pause → timer should never jump incorrectly.
    
- Reset while running → should stop and reset time cleanly.
    
- Timer crossing 59:59 → should continue to 60:00, 60:01, etc.
    
- If the tab becomes inactive, time should not “speed up” when user returns.
    
- If user repeatedly pauses/starts in milliseconds interval → state must remain correct.
    

---

# **💬 Expected Output Behavior**

- Timer increments smoothly every second.
    
- Interface stays stable even if user clicks quickly.
    
- Buttons update the timer logically.
    
- Display always stays in correct mm:ss format.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you implement a countdown timer instead of count up?
    
2. How would you store elapsed time in localStorage so timer restores after reload?
    
3. How would you animate the ticking (bounce / flash)?
    
4. How would you test timer logic in unit tests?
    
5. How would you avoid drift caused by `setInterval` inaccuracies?
    

---

# 🌟 Innovative Ideas (Bonus Points)

- Add lap recording (“Lap 1: 00:23”).
    
- Add smooth digit transition animations.
    
- Add keyboard controls:
    
    - Space = Start/Pause
        
    - R = Reset
        
- Add haptic feedback on mobile.
    
- Show time in hours automatically when needed.
    
- Add dark/light mode for the timer.
    

---

If you want, I can prepare **Round 10 — Toast Notifications**, **Round 11 — File Upload**, **Round 12 — Infinite Scroll**, **Round 13 — Virtualized List**, or even backend machine coding patterns. Just tell me!