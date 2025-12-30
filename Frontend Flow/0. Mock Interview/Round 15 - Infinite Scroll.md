Alright Rahul, here comes a clean, interview-grade **mock machine coding question** for **Infinite Scroll** — a favorite for frontend interviews because it tests event handling, performance, async loading, and UI updates.

---

# ✅ **Mock Interview Question — Infinite Scroll (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 40 minutes

### **🎯 Goal:** Build a list that automatically loads more items as the user scrolls.

---

# **📝 Problem Statement**

You are given an API-like function (or a mock array) that returns data in **pages**.  
Your task is to implement an **Infinite Scroll Component** that:

- Loads initial items
    
- Detects when the user reaches the bottom
    
- Fetches and appends more items
    
- Shows a loading indicator
    
- Prevents duplicate or unnecessary calls
    

Mock API example:

```js
function fetchItems(page, limit = 20) {
  return new Promise(resolve => {
    setTimeout(() => {
      const start = (page - 1) * limit;
      const data = Array.from({ length: limit }, (_, i) => `Item ${start + i + 1}`);
      resolve(data);
    }, 800);
  });
}
```

---

# **💡 Functional Requirements**

### **1️⃣ Initial Load**

- On mount, load the first page of items.
    
- Display items cleanly in a scrollable list or page.
    

### **2️⃣ Scroll Detection**

- When user reaches bottom (or near bottom), load next page.
    
- Must avoid:
    
    - Multiple triggers
        
    - Spamming API
        
- Implementation options:
    
    - scroll event listener
        
    - IntersectionObserver (recommended)
        

### **3️⃣ Append New Items**

- Keep adding new items at the bottom as they load.
    
- Ensure smooth UX without flicker.
    

### **4️⃣ Loading Indicator**

- Show a “Loading…” spinner when fetching.
    
- Hide it once data arrives.
    

### **5️⃣ End of List**

- When API returns no more items:
    
    - Stop loading further
        
    - Show “No more items” or nothing
        

### **6️⃣ Clean UI**

- Items should be spaced and easy to read.
    
- Scrolling should feel smooth.
    
- List should not jump around.
    

---

# **🧪 Edge Cases to Handle**

- Scroll event firing too many times → debounce/throttle/flags required.
    
- User scrolls extremely fast → load should still happen once per page.
    
- API errors → show fallback message.
    
- Slow API → show loading indicator but don’t freeze UI.
    
- Very long lists (5000+ items) → consider performance:
    
    - DOM recycling or virtualization (optional)
        
- Empty list on first load → show “No items found.”
    
- User reaches bottom before API finishes → should not trigger multiple loads.
    
- If IntersectionObserver used:
    
    - Should disconnect after reaching end-of-list.
        
    - Should reattach if list updates.
        

---

# **💬 Expected Output Behavior**

- Items appear immediately for first page.
    
- Scrolling down automatically loads newer pages.
    
- Smooth, controlled loading behavior.
    
- No repeated data or flickering.
    
- Spinner appears only during loading.
    
- Graceful end-of-list message.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you implement virtualization to optimize DOM performance?
    
2. How would you use IntersectionObserver instead of scroll event?
    
3. How would you combine infinite scroll with server-side pagination?
    
4. How would you add filters/search to this infinite list?
    
5. How would you cancel pending API requests when new ones start?
    
6. How would you show skeleton loaders instead of “Loading…”?
    

---

# 🌟 Innovative Ideas (Bonus Points)

- Add skeleton loading shimmer instead of spinner.
    
- Add “Scroll to top” floating button.
    
- Add auto-retry if API fails.
    
- Add pull-to-refresh for mobile.
    
- Add animation when new items appear.
    
- Add threshold (load items early to avoid blank window).
    
- Add memoized caching per page.
    

---

If you want the next one, I can prepare:

➡️ **Round 16 — File Upload**  
➡️ **Round 17 — Virtualized List**  
➡️ **Round 18 — Calendar Date Picker**  
➡️ **Round 19 — Drag and Drop**  
➡️ **Round 20 — Tooltip / Popover Advanced**

Just tell me the next round!