Alright Rahul, here comes a sharp, interview-style **mock machine coding round question** for a **Stopwatch Component**.  
This is slightly trickier than a timer because milliseconds need careful handling and clean UI updates.

---

# ✅ **Mock Interview Question — Stopwatch (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 35 minutes

### **🎯 Goal:** Build a **Start / Stop / Reset** stopwatch with **millisecond precision**.

---

# **📝 Problem Statement**

Create a **Stopwatch Component** that:

- Starts counting upward
    
- Stops when requested
    
- Resets to zero
    
- Displays time in this format:
    

```
mm:ss:ms
```

Where:

- `mm` → minutes (00–∞)
    
- `ss` → seconds (00–59)
    
- `ms` → milliseconds (000–999)
    

The stopwatch should feel responsive and smooth.

---

# **💡 Functional Requirements**

### **1️⃣ Start**

- Clicking **Start** begins counting immediately.
    
- Should update milliseconds smoothly (every ~10ms or 1ms depending on your approach).
    
- Clicking Start when already running shouldn’t start multiple timers.
    

### **2️⃣ Stop**

- Clicking **Stop** pauses the stopwatch.
    
- Clicking Start again should continue from exact paused time.
    
- No drifting or jumping allowed.
    

### **3️⃣ Reset**

- Clicking **Reset**:
    
    - Stops the stopwatch
        
    - Sets time to **00:00:000**
        
    - Clears all running intervals
        

### **4️⃣ Display Format**

- Must always show zero-padded values:
    
    - `09:02:004`
        
    - `00:00:000`
        
    - `01:59:999`
        

### **5️⃣ Performance**

- Updates should feel smooth, not choppy.
    
- No unnecessary re-renders or lag.
    

---

# **🧪 Edge Cases to Handle**

- Multiple fast Start clicks → no duplicate intervals.
    
- Stop then Start must resume without losing or gaining time.
    
- Reset during running → should fully restart at 00:00:000.
    
- Long running times (10+ minutes) → no overflow or display issues.
    
- Milliseconds must not “freeze” when the tab is inactive.
    
- Time drift:
    
    - Avoid relying solely on setInterval(1)
        
    - Prefer calculating time based on real timestamps
        
- Stopwatch should not “jump ahead” when the browser throttles intervals.
    

---

# **💬 Expected Output Behavior**

- Stopwatch digits update cleanly.
    
- Milliseconds feel smooth and natural.
    
- Start/Stop/Reset buttons respond instantly.
    
- The display stays accurate and zero-padded.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you ensure millisecond accuracy despite setInterval throttling?
    
2. How would you synchronize stopwatch state across tabs?
    
3. How would you store time in localStorage so it survives page refresh?
    
4. How would you animate digit changes?
    
5. How would you design this as a reusable hook (e.g., `useStopwatch`)?
    

---

# 🌟 Innovative Ideas (Bonus to Impress)

- Add **lap recording** (Lap 1, Lap 2…).
    
- Add **circle indicator** that fills as seconds pass.
    
- Add **keyboard shortcuts**:
    
    - Space = Start/Stop
        
    - R = Reset
        
    - L = Add Lap
        
- Add **split view** for comparing lap times.
    
- Add smooth fade/slide transitions for time digits.
    
- Add optional sound for each second tick.
    

---

If you want, we can move to **Round 11 — File Upload**, **Round 12 — Toast Notifications**, **Round 13 — Infinite Scroll**, **Round 14 — Virtual List**, or full-stack rounds next. Just tell me and I’ll build the next question!