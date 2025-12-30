Alright Rahul, let’s set up a clear and interview-ready **mock machine coding question** for the **Accordion Component** pattern. I’ll make it simple to read, realistic, and full of smart edge cases so you train at a higher level.

---

# ✅ **Mock Interview Question — Accordion Component (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 30 minutes

### **🎯 Goal:** Build an accordion with expand/collapse behavior.

---

# **📝 Problem Statement**

You need to build an **Accordion component** for a FAQ page.  
Each panel has a **title** and **content**.  
When the user clicks a panel header:

- It should **expand** if closed.
    
- It should **collapse** if open.
    
- **Exactly one panel must remain open at any time**.
    

The transition from closed → open should be **smooth and animated**.

You will receive data like:

```js
const items = [
  { id: "q1", title: "What is an accordion?", content: "An accordion displays content in collapsible sections." },
  { id: "q2", title: "How does it work?", content: "Click a header to toggle the visibility of associated content." },
  { id: "q3", title: "Where is it used?", content: "Commonly used in FAQ pages." }
];
```

Render the accordion based on this structure.

---

# **💡 Functional Requirements**

### **1️⃣ Single Open Panel**

- Only **one** panel can be open at a time.
    
- Clicking another panel should close the previous one and open the new one.
    

### **2️⃣ Toggle Behavior**

- Clicking the already open panel should close it, and **no panel remains open**.
    

### **3️⃣ Smooth Animation**

- The expand/collapse must feel smooth:
    
    - Can use CSS transitions.
        
    - Height animation should not feel jumpy.
        

### **4️⃣ Accessibility**

- Entire header must be clickable.
    
- Keyboard support:
    
    - `Enter` / `Space` → toggle open/close
        
    - `ArrowDown` → focus next panel
        
    - `ArrowUp` → focus previous panel
        

---

# **🧪 Edge Cases to Handle**

- **Empty list** → show “No items available”.
    
- Panel with **missing title** → show “Untitled”.
    
- Panel with **missing content** → still expand but show a blank area.
    
- Extremely long content → should not break animation (use `max-height` or auto-measure).
    
- Multiple panels having the same ID → treat IDs only for internal reference, not uniqueness.
    
- If content fetch is async:
    
    - Show “Loading…” while content loads.
        
- If user double-clicks very fast → animation shouldn’t glitch.
    
- Should handle mobile:
    
    - Text wrap okay.
        
    - Headers clickable easily.
        

---

# **💬 Expected Output Behavior**

- Accordion should feel smooth and polished.
    
- Properly transitions open/close.
    
- Only one open at a time unless user closes all.
    
- Clean and readable layout.
    
- Works with both mouse and keyboard.
    

---

# ⭐ **Interviewer Follow-Up Questions**

1. How would you make the accordion reusable across different pages?
    
2. How would you support multiple open panels at once?
    
3. How would you animate height without hardcoding?
    
4. How would you make the accordion accessible (ARIA roles)?
    
5. How would you lazy-load content only when panel opens?
    
6. How would you track open panel in URL or localStorage?
    

---

# 🌟 Innovative Ideas (Bonus for Impressing Interviewers)

- Add rotating arrow icons (smooth rotation on open).
    
- Add shadow animation while expanding.
    
- Add auto-scroll to keep opening panel in view.
    
- Add “Open All / Close All” button for power users.
    
- Add theme support (dark/light).
    
- Add swipe gestures on mobile to collapse.
    

---

If you want next rounds — **Carousel, Modal, Infinite Scroll, File Upload, Virtualized List, Toast Notifications, Drag & Drop, etc.** — I can prepare them with the same quality.