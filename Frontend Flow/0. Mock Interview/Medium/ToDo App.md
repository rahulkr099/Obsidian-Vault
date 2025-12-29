Alright Rahul — here is the **premium-quality mock interview question** for the **MOST ASKED frontend machine coding round:**  
The **TODO Application** with filtering + localStorage + editing + drag-and-drop.

This version includes:

✔ Functional requirements  
✔ UI requirements  
✔ Data flow  
✔ Edge cases  
✔ Failure scenarios  
✔ Acceptance criteria  
✔ Test cases  
✔ Bonus tasks

This is the EXACT level used by:

**Swiggy, Zomato, Razorpay, Meesho, PhonePe, Flipkart, CRED, Paytm, Hotstar, Startups**

Let’s build your interview prep properly.

---

# 🚀 **🔥 MACHINE CODING ROUND – FULL TODO APPLICATION**

## ⏱ Duration: 45–60 minutes

## 🧪 Difficulty: Medium

## 🧰 Tech: HTML + CSS + JavaScript (No frameworks)

---

# 📝 **📌 Problem Statement**

Build a **TODO application** with:

- Add todo
    
- Delete todo
    
- Mark todo as completed
    
- Filter todos by **All / Active / Completed**
    
- Persist todos using **localStorage**
    
- Reorder todos using **drag & drop**
    
- Edit todo on **double-click**
    

This is the **#1 most asked machine coding question** for frontend roles.

---

# 🎯 **📋 Functional Requirements**

## 1️⃣ Add Todo

- Input field + Add button
    
- Add on ENTER key also
    
- If input empty → do nothing
    

## 2️⃣ List Todos

Each todo item must show:

- checkbox (completed toggle)
    
- text
    
- delete button
    

## 3️⃣ Delete Todo

- Clicking delete removes the item
    
- Should update localStorage
    
- No confirmation popup required
    

## 4️⃣ Mark Completed

- Clicking checkbox toggles completed
    
- Completed todos show **line-through**
    
- Should immediately update UI + localStorage
    

## 5️⃣ Filters

Three filter buttons:

- **All** → show all todos
    
- **Active** → only incomplete
    
- **Completed** → only done
    

The selected filter button should be **highlighted**.

## 6️⃣ Persist in localStorage

Store:

```
[{ id, text, completed, order }]
```

On refresh → UI restores perfectly.

## 7️⃣ Edit Todo

- Double-click on a todo → turns into input
    
- ENTER → save
    
- ESC → cancel edit
    
- Save in localStorage
    

## 8️⃣ Drag & Drop Reordering

- Drag todos to reorder
    
- New order must persist in localStorage
    

---

# ⚠️ **📌 EDGE CASES (Very important)**

### Adding Todo:

- Leading/trailing spaces → must trim
    
- Empty after trim → show error or ignore
    
- Max length (optional 80 chars)
    
- Adding duplicate todo text → allowed or not (specify)
    

### Editing Todo:

- Editing to empty string → reject
    
- Clicking outside while editing → auto-save or cancel (pick one)
    
- Editing a completed todo → allowed or not
    

### Deleting Todo:

- Delete last remaining todo → empty state UI should appear
    
- Delete while filtered → correct list should remain
    

### Filtering:

- No active todos → show “No active todos”
    
- No completed todos → show “No completed todos”
    
- Switching filters should NOT reset scroll position
    

### Drag & Drop:

- Dragging first to last
    
- Dragging last to first
    
- Dragging completed → allowed or not
    
- Invalid drag → ignore
    

### localStorage:

- Corrupted data → reset automatically
    
- Large input → reject
    
- Inconsistent IDs → regenerate
    

---

# 💥 **📌 FAILURE SCENARIOS**

You must handle gracefully:

- localStorage disabled or full → fallback to in-memory todos
    
- User deletes todo while editing another
    
- Dragging while editing → editing should exit cleanly
    
- Double-click too fast → should not break
    
- Slow device → UI must not freeze
    

---

# 🎯 **📌 ACCEPTANCE CRITERIA**

Your solution will be ACCEPTED only if:

### UI:

- Clean
    
- Mobile responsive
    
- Smooth drag + drop
    
- Filters visually clear
    
- Editing seamless
    

### Code Quality:

- Separate functions: addTodo, deleteTodo, filterTodos, renderTodos, saveToLocalStorage
    
- No duplicated code
    
- Good naming
    
- Modular file structure
    
- No global pollution
    
- No inline HTML event attributes
    

### Behavior:

- Realtime updates
    
- No page refresh
    
- Instant localStorage sync
    
- Edit & drag features stable
    

### Performance:

- Re-render must be efficient
    
- Avoid unnecessary DOM rebuilds
    

---

# 🧪 **📌 Test Cases**

|Action|Expected Output|
|---|---|
|Add “Buy milk”|Todo appears|
|Add “ Learn JS ”|Saves as “Learn JS”|
|Mark “Buy milk” completed|Shows line-through|
|Filter = Active|Shows only incomplete|
|Filter = Completed|Shows only completed|
|Double-click “Buy milk” → edit → change to “Buy bread”|Text updates|
|Press ESC during edit|Cancels edit|
|Drag item #3 to top|Order updates instantly|
|Refresh page|Same order + same data|
|Delete “Buy bread”|Removed from UI + localStorage|
|Delete all items|Empty state UI|
|Edit to empty and press ENTER|Error OR ignore (must decide)|

---

# ⭐ **📌 Bonus (Optional for extra marks)**

- Add “Clear Completed” button
    
- Add dark mode
    
- Animate drag & drop
    
- Add date/time when todo was created
    
- Add categories/tags
    
- Add undo delete
    

---

# 🎤 **📌 Interviewer Notes (What they evaluate)**

- Structure of code
    
- Consistent naming
    
- Modular functions
    
- Correct use of event delegation
    
- Minimal DOM operations
    
- Stability of drag & drop
    
- Correct state management
    
- Clean UI
    
- No console errors
    
- No buggy behavior
    
- Quick iteration speed
    
- Calmness + clarity
    
- LocalStorage reliability
    

---

# Rahul, this is EXACTLY how real companies test Todo apps in machine coding rounds.

If you want:

👉 I can start this as a **live mock round**  
👉 I can generate a **starter template**  
👉 I can give the **complete working solution**  
👉 I can create **system design for Todo backend version**  
👉 I can create **React version**  
👉 I can create **Full-stack version**

Just tell me:

### **Start this mock round**

or

### **Give me the solution**