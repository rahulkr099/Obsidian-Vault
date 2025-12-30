Alright Rahul, here comes a solid, interview-level **mock machine coding question** for a **Virtualized List (Windowing)** — a favorite in frontend rounds when they want to test performance thinking.

---

# ✅ **Mock Interview Question — Virtualized List (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 50 minutes

### **🎯 Goal:** Render **only the visible items** from a very large list to improve performance.

---

# **📝 Problem Statement**

You are given a very large list — for example:

```js
const items = Array.from({ length: 100000 }, (_, i) => `Item ${i + 1}`);
```

Rendering all 100,000 items at once will freeze the UI.  
Your task is to build a **Virtualized List Component** (also called “windowing”) that:

- Shows **only items visible in the viewport**
    
- Calculates and maintains correct item positions
    
- Smoothly scrolls without lag
    
- Preserves correct total scroll height
    

---

# **💡 Functional Requirements**

### **1️⃣ Fixed Item Height**

- Assume each item has the same height (e.g., 40px).
    
- Use this to calculate how many items can fit in the viewport.
    

### **2️⃣ Visible Window Rendering**

- Only render items that should be visible:
    
    - Based on scroll position
        
    - Plus a small buffer above/below (optional but smooth)
        

### **3️⃣ Container Height**

- Even though only a few items are rendered:
    
    - The container’s total scrollable height must represent full list
        
    - Example:
        
        ```
        totalHeight = items.length * ITEM_HEIGHT
        ```
        

### **4️⃣ Absolute Positioning**

- Each rendered item must be placed using `position: absolute; top: Xpx;`
    
- This ensures correct alignment inside the large virtual container.
    

### **5️⃣ Smooth Scroll**

- Scrolling must feel natural.
    
- No jank, no jumps, no visible re-render delays.
    

---

# **🧪 Edge Cases to Handle**

- Very fast scroll → should still calculate correct visible range.
    
- List smaller than viewport → render all items without breaking.
    
- Empty list → show “No items”.
    
- Resize of container (window resize) → recalculate visible items.
    
- Different item heights (optional advanced challenge).
    
- Index calculation must never go below 0 or above list length.
    
- Performance:
    
    - Should not cause unnecessary rerenders.
        
    - Should remain smooth even with 100k+ items.
        

---

# **💬 Expected Output Behavior**

- Only the visible portion of the list appears in DOM.
    
- Scrolling feels smooth with no lag.
    
- Total scroll height is correct.
    
- Items appear at correct positions.
    

Example viewport:

```
|------------------------------|
| Item 450                     |
| Item 451                     |
| Item 452                     |
| ...                          |
| Item 490                     |
|------------------------------|
```

---

# ⭐ Interviewer Follow-Up Questions

1. How would you handle **variable height items**?
    
2. How would you combine virtualization with **infinite scroll**?
    
3. How would you optimize re-renders for React?
    
4. How would you measure item height dynamically?
    
5. How would you implement keyboard navigation inside the virtual list?
    
6. How would you add caching or memoization for scroll positions?
    

---

# 🌟 Innovative Ideas (Bonus Points)

- Add **dynamic resizing** support when items grow/shrink.
    
- Add sticky header inside virtualized area.
    
- Add grouped virtualization (e.g., months, categories).
    
- Add smooth reveal animations when new items appear.
    
- Add scroll-to-index feature.
    
- Add virtualization for both rows + columns (grid virtualization).
    

---

If you want, I can prepare:

➡️ **Round 18 — File Upload**  
➡️ **Round 19 — Calendar / Date Picker**  
➡️ **Round 20 — Drag & Drop Sorting**  
➡️ **Round 21 — Chat UI (WhatsApp-like)**  
➡️ **Backend patterns next**

Just tell me the next one!