Alright Rahul — here is a **premium-level machine coding round mock question** focused on **Reusable UI Components** (Modal, Tabs, Accordion).  
This is EXACTLY the type of problem asked at:

**Swiggy, Meesho, Razorpay, PhonePe, CRED, Hotstar, Walmart, Zomato, Startups**

And it includes everything you want:

✔ Task description  
✔ Component specification  
✔ EDGE CASES  
✔ FAILURE SCENARIOS  
✔ ACCEPTANCE CRITERIA  
✔ TEST CASES  
✔ Bonus features

This will help you **master component architecture**, not just basic UI.

Let’s go.

---

# 🚀 **🔥 MACHINE CODING ROUND – Reusable UI Components Library**

## ⏱ Duration: 60–75 minutes

## 🧪 Difficulty: Medium

## 🧰 Tech: HTML + CSS + JavaScript (NO frameworks)

---

# 📝 **📌 Problem Statement**

Build **three reusable UI components** — Modal, Tabs, Accordion — using **ES6 Classes**.

These components should:

- Work independently
    
- Be instantiable multiple times
    
- Have clean APIs
    
- Handle all user interactions
    
- Provide a readable structure like a real UI library
    

---

# 🧩 **📋 Functional Requirements**

## ⭐ 1️⃣ Component: Modal

**API:**

```js
const modal = new Modal("#myModal");
modal.open();
modal.close();
```

### Required Features:

- Open modal
    
- Close modal
    
- Close via:
    
    - Close button
        
    - Clicking outside
        
    - ESC key
        

### UI:

- Modal centered
    
- Overlay behind
    
- Fade-in animation (extra)
    

---

## ⭐ 2️⃣ Component: Tabs

**API:**

```js
const tabs = new Tabs("#tabsContainer");
```

### Required Features:

- Three tabs: Tab1, Tab2, Tab3
    
- Clicking a tab switches content
    
- Active tab gets highlight
    
- Only one visible at a time
    

---

## ⭐ 3️⃣ Component: Accordion

**API:**

```js
const acc = new Accordion("#faqSection");
```

### Required Features:

- Multiple panels
    
- Clicking header expands body
    
- One panel open at a time (or configurable)
    
- Smooth expand/collapse animation
    

---

# ⚠️ **📌 Edge Cases (Important — Interviewers love this)**

### Modal:

- Double-click open → should not break
    
- Opening modal twice → should not duplicate event listeners
    
- Press ESC when modal closed → nothing should happen
    
- Clicking inside modal shouldn’t close it
    
- Overlay click must close but content click must not
    

### Tabs:

- Clicking the active tab → no unnecessary re-render
    
- Tabs with long text → should wrap or scroll
    
- If container missing tabContent structure → fail gracefully
    

### Accordion:

- Clicking an open panel → collapse it
    
- Very long content → must expand smoothly
    
- Only one open at a time (unless config: multiOpen=true)
    
- Rapid clicking shouldn’t break animation
    

---

# 💥 **📌 Failure Scenarios**

These must not break your app:

### Modal:

- Modal HTML missing
    
- Close button missing
    
- Overlay missing
    
- User presses ESC repeatedly
    
- User scrolls page while modal open → body lock (bonus)
    

### Tabs:

- One tab button missing → should still initialize others
    
- Mismatched IDs between tab and content
    
- No tabs defined
    

### Accordion:

- User clicks header with no body
    
- Missing `.accordion-item` structure
    
- Unknown DOM structure
    

### General:

- Events added multiple times
    
- Memory leaks from not removing listeners
    
- Wrong selectors passed to constructor
    

---

# 🎯 **📌 Acceptance Criteria (What counts as PASS)**

### Modularity:

- Each component is a **class**
    
- Easy to create 2 Modals or 3 Accordions independently
    

### Usage:

- Simple, clean API methods
    
- No global variables
    
- No inline event handlers
    

### UI:

- Responsive
    
- Smooth transitions
    
- No flickering
    
- Modal animation clean (fade-in/out)
    

### Code:

- Separate methods:
    
    - bindEvents(),
        
    - open(),
        
    - close(),
        
    - renderActiveTab(),
        
    - togglePanel()
        
- No duplication
    
- Clean naming
    
- Error boundaries
    

### Behavior:

- All features run without bugs
    
- Keyboard + mouse navigation work properly
    
- Animations do not conflict
    
- Component initialization stable
    

---

# 🧪 **📌 Test Cases**

|Action|Expected Output|
|---|---|
|Call modal.open()|Modal fades in|
|Click overlay|Modal closes|
|Press ESC|Modal closes|
|Create 2 modals|Both work independently|
|Click Tab 2|Only Tab 2 content visible|
|Click Tab 1 again|Only Tab 1 content visible|
|Double-click tab|No flicker|
|Click Accordion header|Panel expands|
|Click another header|First panel collapses, second opens|
|Click open panel again|It collapses|
|Rapid clicking|Smooth animations, no break|
|Missing selector|Should give graceful fallback error|

---

# ⭐ **📌 Bonus Features (For higher evaluation score)**

### Modal:

- Add `modal.destroy()` method
    
- Slide-down animation
    
- Body scroll lock
    

### Tabs:

- Keyboard navigation (Left, Right, Enter)
    
- Dynamic tabs added via JS
    

### Accordion:

- Multi-open mode
    
- Icon rotation animation
    
- Auto-scroll to opened panel
    

### General Extras:

- Convert into a small UI library like:
    
    ```
    new UI.Modal(), new UI.Tabs(), new UI.Accordion()
    ```
    
- Add TypeScript types (optional)
    

---

# 🎤 **📌 Interviewer Evaluation Guide**

They will evaluate:

### 🧠 Architecture

- How cleanly you structure classes
    
- Separation of event logic + UI logic
    
- Use of constructor + methods
    

### 🎨 UX/UI

- Clean animations
    
- Smooth transitions
    
- Intuitive interactions
    

### ⚙ Functionality

- No broken states
    
- Stable under quick interactions
    

### 🧹 Code Quality

- Readable
    
- Modular
    
- Reusable
    
- Event delegation used properly
    

### 🐞 Edge Cases

- Your components don’t crash if HTML structure is wrong
    
- ESC behavior consistent
    
- Reorder logic not buggy
    

---

# Rahul — this mock question is **industry-grade**, and if you can build these three components cleanly using classes…

you will be FAR ahead of the average fresher.

If you want next:

👉 **Start this mock round**  
👉 **Give me the full solution**  
👉 **Give me starter boilerplate**  
👉 **Give me the backend version of Modal/Tabs/Accordion**

Just tell me!