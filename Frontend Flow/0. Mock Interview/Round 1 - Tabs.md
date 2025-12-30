Alright Rahul, let’s build a **mock interview question** for a frontend **machine coding round** based on the **Tabs Component** pattern. I’ll also sprinkle in some smart edge cases and improvement ideas so you train like a pro.

---

# ✅ **Mock Interview Question — Tabs Component (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 30 minutes

### **🎯 Goal:** Build a multi-tab UI where users can switch between tabs.

---

# **📝 Problem Statement**

You are asked to build a **Tabs component** for a dashboard.  
The UI should display a row of tab buttons and show the content for the currently active tab.

You must implement:

### **1️⃣ Tab Headers**

- Show all tabs horizontally.
    
- Active tab must be visually highlighted.
    
- Clicking a tab changes the active tab.
    

### **2️⃣ Tab Content**

- Show content of only the selected tab.
    
- Hide all other tab contents without destroying them.
    

### **3️⃣ Configurable Tabs**

You will be given an input array like:

```js
const tabs = [
  { id: "home", label: "Home", content: "Welcome to the homepage." },
  { id: "profile", label: "Profile", content: "This is your profile." },
  { id: "settings", label: "Settings", content: "Adjust your preferences." }
];
```

Render your UI based on this.

---

# **💡 Functional Requirements**

### **Core**

- Default to the _first_ tab active.
    
- Highlight the active tab visually.
    
- Clicking a tab should:
    
    - Switch the highlight.
        
    - Update the visible content.
        

### **Accessibility**

- Should support keyboard navigation:
    
    - `ArrowRight` → move to next tab
        
    - `ArrowLeft` → move to previous tab
        
    - `Enter`/`Space` → activate tab
        

---

# **🧪 Edge Cases to Handle**

- If the tabs array is **empty**, show:  
    “No tabs available.”
    
- If a tab has **no label**, show “Untitled”.
    
- If a tab has **no content**, show nothing but still render the tab.
    
- If two tabs have the same ID, only the first one should be used.
    
- If someone passes an extremely large content string, the UI shouldn’t freeze.
    
- If content takes time to load (simulate with setTimeout), show a small loading placeholder like “Loading…”.
    
- Should gracefully handle long tab labels (use ellipsis or wrap).
    

---

# **💬 Expected Output Behavior**

- Smooth switching.
    
- Clear active indicator (background/border).
    
- Content should appear instantly when clicked.
    
- Keyboard-friendly navigation.
    
- Responsive layout (tabs wrap on smaller screens).
    

---

# **🧠 Interviewer Follow-Up Questions**

1. How would you make the Tabs component reusable across the app?
    
2. Can you support icons inside tab headers?
    
3. How would you animate the tab switch?
    
4. How would you handle asynchronous content (API fetch)?
    
5. How would your component scale to hundreds of tabs?
    
6. How would you lazy-load non-active tab content?
    

---

# ⭐ Innovative Ideas (Bonus for Impressing Interviewers)

- Add **sliding underline animation** under the active tab.
    
- Add **tab closing** (like browser tabs).
    
- Add **URL sync** → active tab updates `?tab=profile`.
    
- Add **scrollable tabs** for many headings (like YouTube mobile UI).
    
- Add **drag-to-reorder** tabs.
    
- Add **dark mode smart contrast** for active tab.
    

---

If you want, I can also:

✅ Give the **full solution code** (React/Vanilla/Next.js).  
✅ Convert this into a **full scoring rubric**.  
✅ Create **Round 2, Round 3…** for other patterns.

Just tell me!