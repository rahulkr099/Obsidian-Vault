Alright Rahul, here comes a clean and interview-grade **mock machine coding question** for a **Todo List with Filters**.  
This round is one of the most common frontend tests — it checks CRUD, filtering, clean UI, and state management.

---

# ✅ **Mock Interview Question — Todo List with Filters (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 45 minutes

### **🎯 Goal:** Build a **Todo List application** with Add, Complete, Delete, and Filters.

---

# **📝 Problem Statement**

You must build a **Todo List** UI where users can:

- Add new todos
    
- Mark a todo as completed
    
- Delete a todo
    
- Filter between:
    
    - **All**
        
    - **Active**
        
    - **Completed**
        

The app should update instantly and feel smooth.

Initial todos (optional):

```js
const initialTodos = [
  { id: 1, text: "Learn React", completed: false },
  { id: 2, text: "Build Portfolio", completed: true }
];
```

---

# **💡 Functional Requirements**

### **1️⃣ Add Todo**

- Input box + “Add” button.
    
- Pressing Enter should also add.
    
- If input is empty → ignore.
    
- New todos appear at the top or bottom (your choice).
    

### **2️⃣ Complete Todo**

- Clicking a checkbox toggles completion.
    
- Completed todos should show some style:
    
    - Strike-through
        
    - Faded opacity
        
    - Color change
        

### **3️⃣ Delete Todo**

- Each todo must have a delete/remove icon or button.
    
- Removing should update the list instantly.
    

### **4️⃣ Filters**

Add 3 filter buttons:

- **All** → show everything
    
- **Active** → todos where `completed === false`
    
- **Completed** → todos where `completed === true`
    

Active filter should be visually highlighted.

### **5️⃣ Clean UI**

- Todo list must be readable.
    
- Buttons must be easy to click.
    
- Mobile friendly layout.
    
- Smooth transitions if possible.
    

---

# **🧪 Edge Cases to Handle**

- Adding todo with just spaces → ignore.
    
- Very long todo text → wrap cleanly.
    
- Deleting an item while filtering should not break filter view.
    
- Switching filters should never lose state.
    
- Updating a todo while another filter is active should reflect correctly.
    
- No todos → show a friendly empty state:
    
    - “No todos yet”
        
    - Or different messages per filter:
        
        - “No active tasks”
            
        - “No completed tasks”
            
- IDs must remain unique.
    
- Fast adding/deleting should not cause UI flicker.
    

---

# **💬 Expected Output Behavior**

- Todos react instantly to:
    
    - Adding
        
    - Completing
        
    - Deleting
        
    - Filtering
        
- UI feels smooth, consistent, and visually clear.
    
- Filter buttons switch views immediately.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you store todos in **localStorage** so they persist after refresh?
    
2. How would you implement **edit todo** (double click → edit mode)?
    
3. How would you animate item add/remove?
    
4. How would you handle a huge todo list (virtualization)?
    
5. How would you extract todo logic into custom hooks?
    
6. How would you sync this with a backend API?
    

---

# 🌟 Innovative Ideas (Bonus to Impress)

- Add a **Clear Completed** button.
    
- Add priority levels (Low / Medium / High).
    
- Add deadlines + reminders.
    
- Add drag & drop to reorder tasks.
    
- Add dark/light theme for the todo list.
    
- Add small analytics:
    
    - “Completed: 5 | Active: 3”
        
- Add bulk complete / bulk delete actions.
    

---

Whenever you’re ready, I can prepare:

➡️ **ROUND 13 — File Upload**  
➡️ **ROUND 14 — Toast Notifications**  
➡️ **ROUND 15 — Infinite Scroll**  
➡️ **ROUND 16 — Virtualized List**  
➡️ **Backend machine coding rounds** too!

Just tell me the next round.