Alright Rahul, here comes a polished, interview-style **mock machine coding question** for **Toast Notifications**.  
This round checks timing logic, queue handling, animation, and reusable component design — very common in frontend interviews.

---

# ✅ **Mock Interview Question — Toast Notifications (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 40 minutes

### **🎯 Goal:** Build a **Toast Notification System** with auto-dismiss + manual close.

---

# **📝 Problem Statement**

Create a **Toast Notification Component/System** that can display temporary messages on the screen.

A toast should:

- Appear at the top-right (or bottom-right — your choice)
    
- Auto-dismiss after a few seconds (e.g., 3–5 sec)
    
- Allow manual dismiss on “X” click
    
- Handle multiple toasts stacked cleanly
    

You may be provided a function like:

```js
showToast({
  type: "success", // "error", "info", "warning"
  message: "Profile updated successfully!",
  duration: 3000
});
```

Your job is to build the entire toast system from scratch.

---

# **💡 Functional Requirements**

### **1️⃣ Show Toast**

- Calling `showToast()` should add a new toast to the UI.
    
- Each toast should show:
    
    - An icon (optional)
        
    - A type indicator (success/error/warning/info)
        
    - A message
        
    - A close button (X)
        

### **2️⃣ Auto Dismiss**

- Toast should automatically disappear after `duration` ms.
    
- If duration is not provided → default to 3000ms.
    

### **3️⃣ Manual Dismiss**

- Clicking the close button (X) should instantly remove the toast.
    
- Removing must be smooth.
    

### **4️⃣ Multiple Toasts**

- Multiple toasts appear stacked.
    
- New toasts appear on top (or bottom — your choice).
    
- Stacking should not overlap or jump.
    

### **5️⃣ Smooth Animation**

Optional but highly appreciated:

- Fade-in / slide-in when toast appears.
    
- Fade-out / slide-out when toast disappears.
    

### **6️⃣ Clean UI**

- Toasts should look neat:
    
    - Rounded corners
        
    - Soft shadow
        
    - Type-based color scheme (green/red/yellow/blue)
        

---

# **🧪 Edge Cases to Handle**

- Many toasts triggered at once → list should still be stable.
    
- Toast with long message should wrap nicely.
    
- Rapid triggering shouldn't freeze UI.
    
- Manually closing a toast shouldn’t affect timers of other toasts.
    
- If a toast is manually closed before auto-dismiss → auto timer should clear.
    
- Duration = 0 or negative → treat as no auto-dismiss.
    
- Very large duration value → should still work safely.
    
- If same toast message triggered twice → both must display independently.
    
- Toast queue should not overlap when resizing browser.
    

---

# **💬 Expected Output Behavior**

- New toasts slide/fade in smoothly.
    
- Toasts auto-dismiss automatically after given time.
    
- Toasts stack without shifting awkwardly.
    
- Clicking “X” removes only that toast.
    
- System works with multiple rapid triggers.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you build a `useToast()` hook to trigger toasts from anywhere in the app?
    
2. How would you handle global toast state using Context API or Redux?
    
3. How would you prevent memory leaks with many timers running?
    
4. How would you implement toast priority (e.g., errors stay longer)?
    
5. How would you support actions inside toast (e.g., “Undo” button)?
    
6. How would you animate toasts using CSS transitions or Framer Motion?
    

---

# 🌟 Innovative Ideas (Bonus Points)

- Add progress bar countdown under each toast.
    
- Add swipe-to-dismiss for mobile users.
    
- Add live queue limit (e.g., only 3 visible at a time).
    
- Add pause-on-hover (toast stops closing timer while hovered).
    
- Add dark/light variants automatically.
    
- Add different positions (top-left, bottom-right, center).
    

---

If you’re ready, I can prepare:

➡️ **Round 17 — File Upload Component**  
➡️ **Round 18 — Virtualized List**  
➡️ **Round 19 — Calendar / Date Picker**  
➡️ **Round 20 — Drag & Drop Sorting**

Just tell me the next round!