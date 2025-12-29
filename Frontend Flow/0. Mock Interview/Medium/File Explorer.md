Alright Rahul — here is a **premium-quality mock interview question** focused on **recursion + tree rendering**, one of the MOST IMPORTANT knowledge areas for frontend engineers.

This is EXACTLY the style used by:

**Google (UI), Amazon (UI), Microsoft, Atlassian, Flipkart, Meesho, Razorpay, Hotstar, Startups**

And includes:

✔ Functional requirements  
✔ Recursion expectations  
✔ UI behavior  
✔ Edge cases  
✔ Failure scenarios  
✔ Acceptance criteria  
✔ Test cases

Clear, simple, and interview-ready — just the way you like it.  
Let’s do this.

---

# 🚀 **🔥 MACHINE CODING ROUND – Folder Tree (Recursive Rendering)**

## ⏱ Duration: 45–60 minutes

## 🧪 Difficulty: Medium–Hard

## 🧰 Tech: HTML + CSS + JavaScript

---

# 📝 **📌 Problem Statement**

You are given a **nested JSON object** representing a file system.

Your task is to build a **folder-tree UI** that:

- Renders nested folders & files
    
- Uses **recursion** to handle deep nesting
    
- Allows **expand/collapse** of folders
    
- Shows different icons for files vs folders
    
- Clicking a folder toggles its children
    

---

# 📦 **📌 Sample Input JSON**

```js
const data = [
  {
    name: "src",
    type: "folder",
    children: [
      {
        name: "components",
        type: "folder",
        children: [
          { name: "Header.js", type: "file" },
          { name: "Footer.js", type: "file" }
        ]
      },
      {
        name: "index.js",
        type: "file"
      }
    ]
  },
  {
    name: "package.json",
    type: "file"
  }
];
```

---

# 🧩 **📋 Functional Requirements**

## ⭐ 1️⃣ Render the tree recursively

- Each folder can contain:
    
    - files
        
    - folders
        
    - nested folders inside folders
        

## ⭐ 2️⃣ Expand / Collapse folders

- On clicking a folder name:
    
    - If collapsed → expand
        
    - If expanded → collapse
        

## ⭐ 3️⃣ Show icons

- Folder (closed) → 📁
    
- Folder (open) → 📂
    
- File → 📄
    

## ⭐ 4️⃣ Smooth UI

- Indentation for nesting (left padding)
    
- Collapsing should only hide children, not delete them
    

---

# ⚠️ **📌 Edge Cases (VERY IMPORTANT)**

### Folder Edge Cases:

- Folder with **no children**  
    → show folder icon but clicking does nothing
    
- Folder with **only files**
    
- Folder with **deep nested levels** (10+ levels)
    
- Clicking folder repeatedly fast → should not break
    
- Empty folder name (should handle gracefully)
    

### Rendering Edge Cases:

- Empty data array → show “No files found”
    
- Missing `children` key (invalid structure) → skip gracefully
    
- Unknown type (“symlink”) → treat as file or ignore
    
- Very long names → wrap instead of overflow
    
- Special characters in names → safe rendering
    

### Recursion Edge Cases:

- Deep recursion → ensure no stack overflow (within reason)
    
- Circular reference (rare) → detect or break gracefully
    

---

# ❌ **📌 Failure Scenarios**

Your component must NOT break if:

- JSON contains invalid structure
    
- A folder has `children: null`
    
- A file has unexpected extra keys
    
- User clicks when animation running
    
- User clicks on icon instead of label
    
- Styles fail to load
    
- Icons fail to load (fallback to emoji)
    

---

# 🎯 **📌 Acceptance Criteria (Pass/Fail Rules)**

### Rendering:

- Fully recursive
    
- Correct indentation
    
- Icons correct for each node
    
- Smooth expand/collapse
    

### Behavior:

- Clicking a folder toggles its children
    
- Clicking a file does nothing
    
- Only the clicked folder expands/collapses
    
- No UI flicker
    
- No re-rendering entire tree unnecessarily
    

### Code Quality:

- MUST use recursion
    
- Functions should be clear:
    
    - `renderTree(data, container)`
        
    - `createNode(item)`
        
- No repetitive code
    
- Clean DOM creation
    
- No inline events
    
- No global variable pollution
    

### Stability:

- Works with any valid nested JSON
    
- No console errors
    
- No infinite loops
    
- No broken nodes
    

---

# 🧪 **📌 Test Cases**

|Action|Expected Output|
|---|---|
|Render initial tree|Only top-level visible|
|Click folder “src”|Expand children|
|Click folder “components”|Expand children|
|Click “components” again|Collapse children|
|Click file “Header.js”|Nothing happens|
|Click folder with no children|No error|
|Deeply nested folder|All levels render correctly|
|Provide empty data array|Show “No files found”|
|Provide file-only array|Renders only files|
|Click quickly multiple times|No flicker|
|Long folder names|Wrapped text|
|Invalid item (missing type)|Skip gracefully|

---

# 🌟 **📌 Bonus Features (Optional — adds extra marks)**

- Smooth slide animation for collapse
    
- Lazy loading (expand triggers data fetch)
    
- Keyboard navigation (↑ ↓ Enter)
    
- Right-click menu (Rename / Delete)
    
- Breadcrumb display
    
- Search bar to filter files/folders
    
- Highlight selected file
    

---

# 🎤 **📌 Interviewer Evaluation Points**

They will evaluate:

### Recursion:

- Is recursion used cleanly?
    
- Does each node render using the same logic?
    
- Are base cases well-defined?
    

### DOM Manipulation:

- Efficient node creation
    
- Proper event binding
    
- No redundant re-renders
    

### State Handling:

- Expand/collapse state maintained correctly
    
- Icon toggles properly
    

### Code Structure:

- Modular
    
- Easy to read
    
- Well-separated logic
    

### UI/UX:

- Clean indentation
    
- Clear visual hierarchy
    
- Smooth interactions
    

---

Rahul — this is a **real company-level** tree rendering machine coding problem.

If you want next:

👉 **Start this mock round**  
👉 **Get full solution**  
👉 **Get optimized version**  
👉 **Get React version**  
👉 **Get animated version**  
👉 **Get full file explorer with CRUD**

Just tell me — I’m ready!