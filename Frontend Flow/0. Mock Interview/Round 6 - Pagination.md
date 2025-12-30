Alright Rahul, here comes a clean, strong, interview-ready **mock machine coding question** for the **Pagination Component**. This round tests state management, dynamic UI, boundaries, and handling large lists — all very common in real frontend interviews.

---

# ✅ **Mock Interview Question — Pagination (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 40 minutes

### **🎯 Goal:** Build a **Pagination system** that shows a list of items page-by-page.

---

# **📝 Problem Statement**

You are given a large list of items, and you need to build a **Pagination Component** that splits this list into pages and allows the user to navigate using:

- Page numbers
    
- Next / Previous buttons
    
- Disabled navigation at boundaries
    

Create a UI that:

1. Shows only the items for the **current page**.
    
2. Displays page numbers with the **active page highlighted**.
    
3. Supports Next / Previous buttons.
    
4. Handles page limits cleanly.
    

You’ll get something like:

```js
const items = Array.from({ length: 95 }, (_, i) => `Item ${i + 1}`);
const itemsPerPage = 10;
```

---

# **💡 Functional Requirements**

### **1️⃣ Render Page Items**

- Display items only for the active page.
    
- First page loads by default.
    

### **2️⃣ Page Navigation**

- Clicking a page number → moves to that page.
    
- Clicking **Next** → moves to next page.
    
- Clicking **Previous** → moves to previous page.
    

### **3️⃣ Disable Buttons**

- On the **first** page → disable **Previous**.
    
- On the **last** page → disable **Next**.
    

### **4️⃣ Active Page Highlight**

- The current page number should be clearly highlighted.
    
- Other pages stay clickable.
    

### **5️⃣ Handling Large Page Sets (Critical)**

For large data (like 1000+ pages), implement:

```
1 … 6 7 8 … 20
```

- Show a compact pagination layout using `...` ellipsis.
    
- Always show:
    
    - First page
        
    - Last page
        
    - Current page
        
    - Pages surrounding the current page (±1 or ±2)
        

(This is optional but extremely valuable during interviews.)

---

# **🧪 Edge Cases to Handle**

- Items array is **empty** → show “No items to display.”
    
- `itemsPerPage` > total items → show all items on one page.
    
- `itemsPerPage` set to 0 or negative → default to 10.
    
- If user clicks disabled buttons, nothing should happen.
    
- If items update dynamically:
    
    - Page should reset or stay in a valid range.
        
- Handle extremely large lists (say 50,000+ items):
    
    - Pagination should not freeze.
        
    - Page count UI should be optimized (don’t render every page button literally).
        

---

# **💬 Expected Output Behavior**

- Page content updates cleanly.
    
- Pagination bar renders properly and stays stable.
    
- Buttons enable/disable correctly.
    
- Active page is clearly visible and easy to click.
    
- Smooth switching without jumps or layout flicker.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you implement **server-side pagination**?
    
2. How would you fetch new items when page changes?
    
3. How would you handle **infinite scroll pagination**?
    
4. How would you optimize pagination for 100k items?
    
5. Can you transition between pages smoothly (animation)?
    
6. How would you add **keyboard navigation** (arrow keys to switch pages)?
    

---

# 🌟 Innovative Ideas (Bonus to Impress)

- Add **Page Size Selector** (10 / 20 / 50 per page).
    
- Add **Go to page** input box.
    
- Add keyboard arrows for switching pages.
    
- Add animated slide transitions between pages.
    
- Add accessibility:
    
    - ARIA labels
        
    - Focus ring for active element
        
- Add responsive layout:
    
    - Compact version for small screens.
        

---

If you want, I can prepare **ROUND 7 — Tooltip**, **ROUND 8 — Toast**, **ROUND 9 — File Upload**, **ROUND 10 — Carousel**, or even full-stack machine coding rounds next. Just tell me — we keep levelling up!