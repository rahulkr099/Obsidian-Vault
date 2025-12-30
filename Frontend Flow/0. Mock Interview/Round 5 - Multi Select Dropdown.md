Alright Rahul, here comes a clean and realistic **mock machine coding question** for a **Multi-Select Dropdown**. This round is a level up from the single-select dropdown because it challenges your handling of multiple states, chips, selection limits, and interactions.

---

# ✅ **Mock Interview Question — Multi-Select Dropdown (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 40 minutes

### **🎯 Goal:** Build a **fully functional multi-select dropdown** with checkboxes OR chip-style selections.

---

# **📝 Problem Statement**

You need to build a **Multi-Select Dropdown component** that allows users to pick **multiple items** from a list.

The dropdown must:

- Open/close on click.
    
- Show selected items as **checkboxes** or **chips** (your choice).
    
- Allow selecting and deselecting unlimited items (unless restricted).
    
- Close when the user clicks **outside**.
    

You will receive structured options like:

```js
const options = [
  { id: 1, label: "HTML" },
  { id: 2, label: "CSS" },
  { id: 3, label: "JavaScript" },
  { id: 4, label: "React" }
];
```

Render the dropdown based on this.

---

# **💡 Functional Requirements**

### **1️⃣ Dropdown Behavior**

- Clicking the main box → toggle open/close.
    
- Clicking outside → must close the dropdown.
    
- Clicking inside → should NOT close the dropdown.
    

### **2️⃣ Selection Behavior**

Two variants are allowed (pick one during interview):

- **Checkbox-style**: Each option has a checkbox.
    
- **Chips-style**: Selected items appear as removable chips above the input.
    

Selection rules:

- Click on an item → select it.
    
- Click on it again → deselect it.
    
- Selected items should remain highlighted.
    
- Dropdown should reflect the count:  
    **Example:** “3 selected”
    

### **3️⃣ Chips (If chosen)**

- Each selected item must appear as a pill.
    
- Clicking “X” on a chip → removes that selection.
    
- Removing a chip must also update the dropdown state.
    

### **4️⃣ Keyboard Support (Optional but strong bonus)**

- `ArrowDown` / `ArrowUp` → navigate items
    
- `Enter` → toggle selection
    
- `Escape` → close dropdown
    
- `Backspace` on empty input → remove last chip
    
- Type-ahead filtering (optional but impressive)
    

### **5️⃣ Search Filtering (Optional)**

- A small input box inside dropdown that filters shown options while typing.
    

---

# **🧪 Edge Cases to Cover**

- **Empty options list** → show “No options available”.
    
- Options with **identical labels** → must still be selectable independently using IDs.
    
- Very long option names → wrap or truncate cleanly.
    
- Extremely long list → scroll the options with a max-height.
    
- Selecting a huge number of options → chips should wrap to next line without breaking layout.
    
- Clicking scrollbar inside dropdown → should NOT trigger outside click close.
    
- Fast repeated clicks on checkboxes → no double selection bug.
    
- If maximum selection limit is added (optional):
    
    - Selecting beyond limit should disable remaining options.
        
- Dropdown popped near bottom of screen:
    
    - List should scroll instead of overflowing outside the viewport.
        

---

# **💬 Expected Output Behavior**

- Smooth open/close animation.
    
- Clear checkbox or chip-based selection.
    
- Clicking outside instantly closes dropdown.
    
- Selected values displayed clearly in main input area.
    
- Scrollable option list for large data.
    
- Clean interaction and no flickers.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you support **Select All / Deselect All**?
    
2. How would you optimize it for **10,000+ items**?
    
3. Can you make dropdown list render **above** if there’s no space below?
    
4. How would you implement **search + async API filtering**?
    
5. How would you manage **keyboard interactions** across chips + list?
    
6. How would you animate the dropdown and chips?
    

---

# 🌟 Innovative Ideas (Bonus Points to Impress)

- Add tags like “Most used”, “Recommended”.
    
- Add option groups with collapsible categories.
    
- Add a select counter: “Selected (4)”.
    
- Add right-side icons (tick, star, custom icons).
    
- Add multi-level dropdown with subcategories.
    
- Add mobile-friendly large-touch item spacing.
    
- Add virtualized list for huge datasets.
    

---

If you want, I can prepare **ROUND 6 — Tooltip**, **ROUND 7 — Toast**, **ROUND 8 — File Upload**, **ROUND 9 — Table with Sorting**, and more.  
Just tell me — we can build a full machine-coding interview bank!