Alright Rahul, here comes a strong, interview-style **mock machine coding round question** for a **Table with Sorting + Filtering**.  
This round checks data handling, sorting logic, filtering logic, UI design, and performance — one of the most asked questions in frontend interviews.

---

# ✅ **Mock Interview Question — Table Sorting + Filtering (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 50 minutes

### **🎯 Goal:** Build a **data table** that supports:

- Searching
    
- Sorting (ASC/DESC)
    
- Clean row display
    

---

# **📝 Problem Statement**

You are given a dataset of users.  
Your task is to build a **Table Component** with:

- Search (global text filter)
    
- Sortable columns (ASC / DESC toggle)
    
- Clean, responsive UI
    

Example data:

```js
const users = [
  { id: 1, name: "Rahul Sharma", age: 23, city: "Delhi" },
  { id: 2, name: "Aarav Mehta", age: 28, city: "Mumbai" },
  { id: 3, name: "Sneha Gupta", age: 21, city: "Bangalore" },
  { id: 4, name: "Ishita Verma", age: 27, city: "Chennai" }
];
```

Columns to display:

- ID
    
- Name
    
- Age
    
- City
    

---

# **💡 Functional Requirements**

### **1️⃣ Table Display**

- Display data in rows and columns.
    
- Structure should be clean and readable.
    
- Must handle 10–500+ rows smoothly.
    

### **2️⃣ Sorting**

- Clicking a column header toggles between:
    
    - ASC
        
    - DESC
        
    - DEFAULT (unsorted) — optional
        
- Must sort based on data type:
    
    - Strings → alphabetical
        
    - Numbers → numeric
        

Sorting rules:

- Clicking same column cycles:  
    `ASC → DESC → reset` (optional)
    
- Sorting must not mutate the original dataset.
    

### **3️⃣ Search (Global Filter)**

- Input box at top.
    
- Filters through **all fields**, case-insensitive.
    
- Example: searching for “del” should match “Delhi”.
    
- Searching reduces rows dynamically.
    

### **4️⃣ No Results State**

- If no rows match → show:  
    **“No matching results.”**
    

### **5️⃣ Highlighting (Optional but nice)**

- Bold or color the matching parts of text when searching.
    

### **6️⃣ Clean UI**

- Proper column alignment.
    
- Hover state on row.
    
- Sorting arrow indicator (↑↓).
    
- Table should feel light and responsive.
    

---

# **🧪 Edge Cases to Handle**

- Search term empty → show full list.
    
- Search term with spaces → trim before filtering.
    
- Multiple words in search → match any part.
    
- Sorting after searching → must apply to filtered data.
    
- Searching after sorting → must apply to sorted data.
    
- Sorting numeric values must handle:
    
    - 0
        
    - very large numbers
        
    - negative numbers
        
- Sorting string values must:
    
    - Ignore letter case
        
    - Handle undefined or null safely
        
- Very large dataset (1000+ rows):
    
    - No lag
        
    - Efficient sort and filter
        
- Stable sort (optional):
    
    - If sort values equal → maintain original order.
        

---

# **💬 Expected Output Behavior**

- Table updates instantly on each search or sort.
    
- Sort indicators switch correctly.
    
- Combined operations (sort + search) work seamlessly.
    
- No visual glitches.
    
- Rows stay clean, scrollable, and readable.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you optimize filtering + sorting for large datasets?
    
2. How would you implement column-specific filtering (e.g., filter by city only)?
    
3. How would you add pagination on top of this setup?
    
4. How would you extract table logic into reusable hooks?
    
5. How do you ensure stable sorting?
    
6. How would you add server-side sorting & searching?
    

---

# 🌟 Innovative Ideas (Bonus Points)

- Add debounce on search (150–300ms).
    
- Add multi-column sorting (e.g., sort by Name then Age).
    
- Add row selection checkboxes.
    
- Add CSV download button for filtered data.
    
- Add column resizing and drag-reorder.
    
- Add sticky header when scrolling.
    
- Add virtualized table for 10,000+ records.
    

---

If you want, I can prepare:

➡️ **Round 15 — Infinite Scroll**  
➡️ **Round 16 — File Upload**  
➡️ **Round 17 — Virtualized List**  
➡️ **Round 18 — Calendar Picker**  
➡️ **Full-stack machine coding rounds** too!

Just tell me the next one.