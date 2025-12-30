Alright Rahul, let’s set up a neat and interview-style **mock machine-coding question** for the **Dropdown Component**. This round tests interaction handling, state management, and clean UI work — all important for frontend interviews.

---

# ✅ **Mock Interview Question — Dropdown (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 30 minutes

### **🎯 Goal:** Build a **Single-Select Dropdown** with basic interactions and outside-click detection.

---

# **📝 Problem Statement**

You need to build a **custom Dropdown component** without using any UI libraries.

The dropdown must:

- Show a **selected value** in a box.
    
- Open a **list of items** when clicked.
    
- Allow selecting **one** item at a time.
    
- Close when user clicks outside the dropdown area.
    
- Highlight hovered and selected items clearly.
    

You will receive an array like:

```js
const options = [
  { id: 1, label: "Apple" },
  { id: 2, label: "Banana" },
  { id: 3, label: "Cherry" }
];
```

Render your dropdown based on this.

---

# **💡 Functional Requirements**

### **1️⃣ Dropdown Toggle**

- Clicking the main dropdown box → open/close the list.
    
- Clicking outside the component → must close the list.
    

### **2️⃣ Select Item**

- Clicking an item:
    
    - Sets the selected item.
        
    - Highlights it.
        
    - Closes the dropdown.
        

### **3️⃣ Hover Highlight**

- Item should highlight on hover.
    
- When selected, it should stay highlighted even after closing and reopening.
    

### **4️⃣ Keyboard Support (Optional but good)**

- `ArrowDown` → move highlight down
    
- `ArrowUp` → move highlight up
    
- `Enter` → select
    
- `ESC` → close dropdown
    

### **5️⃣ Clean UI**

- Options list should float below the dropdown.
    
- Should not break layout if list is long (scrollable max height).
    

---

# **🧪 Edge Cases to Handle**

- **Empty list** → show “No options”.
    
- If user re-selects the same item, no UI glitch.
    
- Options with **same label** but different IDs—should still work.
    
- Very long labels → should truncate or wrap gracefully.
    
- Dropdown should not close if user scrolls the option list.
    
- Fast clicking shouldn’t break the open/close behavior.
    
- If the dropdown is near the bottom of the screen:
    
    - List should scroll instead of overflowing the viewport.
        
- Clicking on the scrollbar of the dropdown options should NOT trigger outside close.
    

---

# **💬 Expected Output Behavior**

- Smooth open/close.
    
- Clear active and hover highlight.
    
- Clicking outside immediately closes dropdown.
    
- Selected value appears in main box.
    
- Options are easy to scroll and pick on mobile and desktop.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you support multi-select dropdown?
    
2. How would you dynamically load options through an API?
    
3. How would you position the dropdown using portals?
    
4. How would you virtualize 10,000 options without lag?
    
5. How would you animate the dropdown opening?
    

---

# 🌟 Innovative Ideas (Bonus Points)

- Add search inside dropdown (“type to filter”).
    
- Support keyboard type-ahead navigation.
    
- Add icons or images inside options.
    
- Add grouped dropdown sets (fruits, vegetables, etc.).
    
- Add a disabled state for certain options.
    
- Add mobile-friendly tap support with momentum scrolling.
    

---

If you want, I can also give you:

✅ The full solution in JS/React  
✅ Boilerplate code for practice  
✅ Next rounds (like Multi-Select Dropdown, Tooltip, Toast, Carousel, Table, Calendar, etc.)

Just say the word and we roll!