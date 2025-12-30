Alright Rahul, let’s craft a clean and interview-ready **mock machine coding question** for the **Modal / Popup component**. I’ll keep the tone friendly and the structure neat so you can prepare like a real interview session.

---

# ✅ **Mock Interview Question — Modal / Popup (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 30 minutes

### **🎯 Goal:** Build a modal dialog with overlay and multiple closing mechanisms.

---

# **📝 Problem Statement**

You need to build a **Modal / Popup component** that appears on top of the current page with a dark overlay behind it.  
The modal should support **multiple closing methods**, feel clean, and work smoothly across devices.

You will get a trigger button **“Open Modal”**.  
When clicked, the modal must appear with:

- A semi-transparent overlay.
    
- A centered modal box.
    
- A close (“X”) button.
    
- Any content passed inside.
    

Your job is to build the entire modal system from scratch.

---

# **💡 Functional Requirements**

### **1️⃣ Open / Close Behavior**

- Clicking **“Open Modal”** → show modal.
    
- Clicking **X button** → close modal.
    
- Clicking **outside** the modal box (i.e., on overlay) → close modal.
    
- Pressing **ESC key** → close modal.
    

### **2️⃣ UI Requirements**

- Modal should be centered horizontally and vertically.
    
- Overlay should dim the background.
    
- Modal content should stay scrollable when content is large.
    
- Background should be locked (no scrolling) while modal is open.
    

### **3️⃣ Animation (Optional, but recommended)**

- Smooth fade-in for overlay.
    
- Slide or scale animation for modal box.
    

### **4️⃣ Accessibility**

- Focus should move inside the modal when opened.
    
- Pressing TAB should cycle within modal elements only (focus trap).
    
- Modal must have ARIA attributes like:
    
    - `role="dialog"`
        
    - `aria-modal="true"`
        

---

# **🧪 Edge Cases to Handle**

- Opening modal multiple times rapidly should not duplicate DOM elements.
    
- Modal with **no content** should still render box.
    
- If ESC key is pressed when modal is already closed → do nothing.
    
- If modal content is extremely tall:
    
    - Modal body should become scrollable.
        
    - Page behind must remain fixed.
        
- If overlay is transparent or missing, modal should still work.
    
- Clicking inside modal must NOT close it.
    
- If the modal is triggered while another modal is open → only one should be visible.
    
- Multiple trigger buttons pointing to different content should open correct modal (if supporting multi-modal setup).
    

---

# **💬 Expected Output Behavior**

- Dark overlay behind modal.
    
- Modal pops up smoothly without layout shifts.
    
- Modal closes instantly through X, outside click, or ESC.
    
- Focus stays inside modal.
    
- Page behind does not move.
    
- Clean, responsive design on both large and small screens.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you handle multiple modals on the same page?
    
2. How would you implement a focus trap?
    
3. How would you reuse this modal in the entire UI library?
    
4. How would you animate open/close transitions?
    
5. How would you lazy-load modal content?
    
6. How would you test this component?
    

---

# 🌟 Innovative Ideas (Bonus for Impressing Interviewers)

- Add a **Draggable Modal** (user can drag by header).
    
- Add modal stacking with z-index management.
    
- Add **confirmation modal** with action buttons.
    
- Add mobile-friendly modal that slides up from bottom.
    
- Add themed modals (success, error, warning).
    
- Make modal accessible with screen readers (full semantic support).
    

---

If you want, I can also give:

✅ Full solution in Vanilla JS  
✅ Full solution in React  
✅ A full coding test version with starter code and instructions

Just tell me and we continue to next round!