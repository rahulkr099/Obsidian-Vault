Alright Rahul, here comes a crisp and interview-quality **mock machine coding question** for an **OTP Input Boxes Component**.  
This pattern is very popular in interviews because it tests focus management, keyboard handling, and clean UI behavior.

---

# ✅ **Mock Interview Question — OTP Boxes (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 35 minutes

### **🎯 Goal:** Build a 4-digit or 6-digit OTP input system with clean focus behavior.

---

# **📝 Problem Statement**

Create an **OTP Input Component** with **4 or 6 input boxes**, each accepting a single character (0–9 by default).

Users should be able to type OTP seamlessly:

- Typing a digit → auto-moves to next box
    
- Pressing backspace → moves to previous box
    
- Arrow keys → navigate between boxes
    
- Paste full OTP → auto-fills all boxes in order
    

Your component must feel smooth and look clean.

You may get config inputs like:

```js
const length = 6;  // or 4
const type = "number";  // optional "text" or "password"
```

---

# **💡 Functional Requirements**

### **1️⃣ Input Boxes**

- Render **N** boxes (N = 4 or 6).
    
- Each box should allow **only 1 character**.
    
- Should only accept valid characters:
    
    - For numeric OTP → digits 0–9.
        
    - For general OTP → any character (optional).
        

### **2️⃣ Auto Focus Navigation**

- After entering a character:
    
    - Cursor must jump to the next input.
        
- If on last input → stay there.
    

### **3️⃣ Backspace Navigation**

- If box is empty and user presses Backspace → go to previous box.
    
- If box has a value and user presses Backspace → clear the value but stay.
    

### **4️⃣ Paste Support**

- If user pastes a 4/6-digit string:
    
    - Fill boxes left to right.
        
    - Extra characters should be ignored.
        

### **5️⃣ OTP Completion**

- When all boxes are filled:
    
    - Emit final OTP as a string (e.g., “123456”).
        
    - Optional: automatically submit.
        

### **6️⃣ Mobile Friendly**

- Inputs large and tappable.
    
- Numeric keypad opens on mobile for numeric OTP.
    

---

# **🧪 Edge Cases to Handle**

- User types letters when numbers are expected → ignore.
    
- User tries to type more than one character → keep only last digit.
    
- User pastes too long input → crop cleanly.
    
- User pastes fewer characters → fill partially without breaking focus.
    
- Pressing left/right arrow keys → navigate correctly.
    
- Fast typing shouldn’t skip or override boxes.
    
- Clearing all boxes should reset focus to first.
    
- Cursor jumping must remain stable with rapid backspace.
    

---

# **💬 Expected Output Behavior**

- Inputs move smoothly on typing/backspacing.
    
- Pasting fills all boxes in order.
    
- OTP string available when all fields filled.
    
- UI looks clean, centered, and easy to read.
    
- Works perfectly on both desktop and mobile.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you mask OTP securely (like ●●●●)?
    
2. How would you support both number and alphanumeric OTPs?
    
3. How would you add a **timer** + **resend OTP** button?
    
4. How would you validate OTP length before submission?
    
5. How would you make the entire component keyboard-accessible?
    
6. How would you convert this into a reusable `<OtpInput />` component?
    

---

# 🌟 Innovative Ideas (Bonus Points)

- Add automatic paste detection with animation.
    
- Add autofocus on first input when component mounts.
    
- Add success animation when OTP completes (glow/shake).
    
- Add error shake animation when OTP is wrong.
    
- Add theme variants (border styles, filled style).
    
- Add haptic feedback on mobile.
    

---

If you're ready, we can continue to:  
➡️ **Round 14 — File Upload**  
➡️ **Round 15 — Toast Notifications**  
➡️ **Round 16 — Infinite Scroll**  
➡️ **Round 17 — Virtualized List**

Just tell me the next round!