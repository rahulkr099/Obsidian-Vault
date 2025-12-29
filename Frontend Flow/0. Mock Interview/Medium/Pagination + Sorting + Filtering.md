Alright Rahul — here is a **premium-quality, interview-perfect mock machine coding round question** on **Table Rendering + Pagination + Sorting + Search + Filters**.

This is EXACTLY the style used in **Razorpay, Swiggy, Meesho, Amazon (UI), Walmart, PhonePe, Zomato, Hotstar**, and all product-based FE rounds.

I’ve included:

✔ Functional requirements  
✔ UI requirements  
✔ Edge cases  
✔ Failure scenarios  
✔ Acceptance criteria  
✔ Test cases  
✔ Extra filters

This is one of the MOST IMPORTANT patterns in frontend interviews.

Let’s do this cleanly and clearly.

---

# 🚀 **🔥 MACHINE CODING ROUND – Data Table with Pagination, Sorting, Search, Filters**

## ⏱ Duration: 45–60 minutes

## 🧪 Difficulty: Medium

## 🧰 Tech: HTML + CSS + JavaScript (NO frameworks)

---

# 📝 **📌 Problem Statement**

You are given a list of **100 items** (objects).  
Build a **data table** with:

- Pagination (10 rows per page)
    
- Next / Previous navigation
    
- Sorting by a column (A→Z, Z→A)
    
- Search (real-time or button-based)
    
- Optional filters (Category, Price Range)
    

This is a **core frontend skill test**.

---

# 📦 **📌 Sample Data Format**

```js
const products = [
  {
    id: 1,
    name: "Laptop",
    category: "Electronics",
    price: 50000
  },
  {
    id: 2,
    name: "Shoes",
    category: "Fashion",
    price: 2000
  },
  // ... up to 100 items
];
```

---

# 🧩 **📋 Functional Requirements**

## ⭐ 1️⃣ Render table

Columns to display:

- ID
    
- Name
    
- Category
    
- Price
    

Must show **only 10 rows per page**.

## ⭐ 2️⃣ Pagination

- Buttons: Previous, Next
    
- Disable Previous on page 1
    
- Disable Next on last page
    
- Page number display:
    
    ```
    Page 3 of 10
    ```
    

## ⭐ 3️⃣ Sorting

User can sort by **Name**:

- Ascending (A→Z)
    
- Descending (Z→A)
    
- Clicking the same button toggles order
    

### Optional:

- Sort by price
    

---

## ⭐ 4️⃣ Search

Input field filters items by **name**:

- Case-insensitive
    
- Partial match
    
- Works together with pagination (filtered results affect page count)
    
- Updates table immediately
    

---

## ⭐ 5️⃣ Filters (Extra)

### Category filter:

Dropdown:

- All
    
- Electronics
    
- Fashion
    
- Grocery
    
- …
    

### Price range filter:

- Min price
    
- Max price
    

Filters + search + sorting should all work **together**.

---

# ⚠️ **📌 Edge Cases (Very important for interviews)**

### Pagination:

- On applying search → reduce page count automatically
    
- On filter → reset to page 1
    
- Next should NOT go beyond last page
    
- Items < 10 → show only available rows
    

### Search:

- Empty input → show all
    
- Search with spaces → trim
    
- No match → show “No results found”
    
- Search + pagination interaction:
    
    - If search returns 4 items → only 1 page exists
        

### Sorting:

- Sorting empty result → no error
    
- Sorting after search → must still work
    
- Sorting after filter → must still work
    
- Sorting resets pagination to page 1
    

### Filters:

- Min > Max → treat as invalid OR swap (you choose)
    
- Non-numeric price → ignore
    
- Unknown category → ignore
    
- Multiple filters stacking must still reflect accurate results
    

### UI:

- Very long names → wrap text
    
- Table width small → columns adjust cleanly
    

---

# ❌ **📌 Failure Scenarios**

Your solution must not break when:

- Data array empty
    
- Data missing a field (null or undefined)
    
- Category or price fields missing
    
- User resets filters while on last page
    
- Sorting applied on filtered results
    
- Rapid clicking of sort or pagination buttons
    
- Search string includes special characters
    
- User types extremely fast
    

---

# 🎯 **📌 Acceptance Criteria (Pass/Fail Rules)**

### UI:

- Clean table layout
    
- Pagination clearly visible
    
- Search input and buttons neatly placed
    
- No overlapping text
    
- Empty states shown gracefully
    

### Behavior:

- Table updates instantly on search
    
- Sorting toggles correctly
    
- Pagination always accurate
    
- Filters combine with search correctly
    
- No flickering/back-and-forth rendering
    

### Code:

- No inline event handlers
    
- Separate functions:
    
    - renderTable
        
    - paginate
        
    - handleSearch
        
    - handleSort
        
    - applyFilters
        
    - calculatePages
        
- Clear variable names
    
- No global memory leaks
    
- No duplicate code
    
- No console errors
    

### Performance:

- Handle 100 items easily
    
- Efficient filtering + sorting (no heavy loops inside loops)
    

---

# 🧪 **📌 Test Cases**

|Action|Expected Result|
|---|---|
|Initial render|First 10 items|
|Click Next|Page 2 shown|
|On last page → click Next|Disabled, no effect|
|Click Sort A→Z|Table sorted ascending|
|Click Sort again|Sorted descending|
|Search “lap”|Only items with “lap” shown|
|Search “xyz”|“No results found”|
|Apply category = Electronics|Only electronics shown|
|Set min = 1000, max = 5000|Only items in this range|
|Combine search + filter|Correct intersection shown|
|Apply filters → then sort|Sorted within filtered list|
|Search while on page 3|Reset to page 1|
|Remove filter|Full data restored|
|Add extremely long product name|Wrapped, not broken|

---

# 🌟 **📌 Bonus Points (Optional for extra marks)**

- Add page numbers (1 2 3 …)
    
- Add “First” and “Last” buttons
    
- Highlight selected sort direction
    
- Show total results: “23 items found”
    
- Add loading indicator (simulated delay)
    
- Add debounce for search
    
- Add responsive layout
    

---

# 🎤 **📌 Interviewer Evaluation Areas**

### Logic:

- Data flow from filtering → sorting → pagination is correct
    
- No redundant operations
    
- Clean state handling
    

### UI/UX:

- Smooth updates
    
- Clear navigation
    
- Accurate row counts
    

### Code:

- Modular
    
- Clean separation of concerns
    
- Good naming conventions
    

### Edge Case Handling:

- No crashes
    
- No incorrect page counts
    
- Search + filter + sort all stack properly
    

---

Rahul — this is EXACTLY how real table rendering machine coding rounds are tested.

If you want:

👉 Start this mock round  
👉 Get full working solution  
👉 Get optimized version  
👉 Get React version  
👉 Get Tailwind UI version  
👉 Get backend API version (pagination from server)

Just say the word — I’m ready!