Alright Rahul, let’s build a **clean, interview-ready Tabs Component** using **HTML, CSS, and JavaScript**.  
This is one of the easiest but most common machine-coding problems because it tests:

- DOM events
    
- Component structure
    
- State switching
    
- Clean separation of logic + markup
    
- Reusability
    

I'll give you:

✅ Problem statement (exact interview style)  
✅ Full working code (HTML + CSS + JS)  
✅ Extensible tab API  
✅ Extra improvement ideas so you can master the pattern

Let’s roll!

---

# 🚀 **Machine Coding Round Project: Tabs Component**

---

## 📌 **Problem Statement (Interviewer Style)**

Build a Tabs UI where:

- Clicking on a tab should show its content.
    
- Only one tab’s content is visible at a time.
    
- Active tab should be highlighted.
    
- Component should be clean, modular, and scalable for 10+ tabs without extra code changes.
    

---

# 🧱 **FULL WORKING PROJECT**

---

## 📂 Folder structure

```
tabs-project/
│── index.html
│── style.css
└── script.js
```

---

# ✅ **index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tabs Component</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>

    <h1>Tabs Component (Machine Coding Round)</h1>

    <div class="tabs-container">
        <div class="tabs">
            <button class="tab active" data-tab="tab1">Home</button>
            <button class="tab" data-tab="tab2">Profile</button>
            <button class="tab" data-tab="tab3">Settings</button>
        </div>

        <div class="tab-content">
            <div id="tab1" class="content active">Welcome to the Home tab.</div>
            <div id="tab2" class="content">This is your Profile tab.</div>
            <div id="tab3" class="content">Settings tab content goes here.</div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
```

---

# ✅ **style.css**

```css
body {
    font-family: Arial, sans-serif;
    background: #f4f4f4;
    padding: 40px;
}

h1 {
    text-align: center;
    margin-bottom: 25px;
}

.tabs-container {
    max-width: 600px;
    margin: 0 auto;
    background: white;
    border-radius: 10px;
    padding: 20px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.tabs {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
}

.tab {
    padding: 10px 20px;
    border: none;
    background: #eee;
    cursor: pointer;
    border-radius: 6px;
    font-size: 16px;
}

.tab.active {
    background: black;
    color: white;
}

.content {
    display: none;
    font-size: 18px;
    padding: 10px 0;
}

.content.active {
    display: block;
}
```

---

# ✅ **script.js**

```javascript
const tabs = document.querySelectorAll(".tab");
const contents = document.querySelectorAll(".content");

tabs.forEach(tab => {
    tab.addEventListener("click", () => {
        const target = tab.getAttribute("data-tab");

        // Remove active from all tabs
        tabs.forEach(t => t.classList.remove("active"));

        // Add active to clicked tab
        tab.classList.add("active");

        // Hide all content
        contents.forEach(c => c.classList.remove("active"));

        // Show target
        document.getElementById(target).classList.add("active");
    });
});
```

---

# 🎯 **Interview-Ready Explanation (You Can Speak This)**

- Tabs are selected using a `data-tab` attribute.
    
- When a tab is clicked, I:
    
    - Remove the active class from all tabs
        
    - Add it to the clicked tab
        
    - Hide all content blocks
        
    - Show the content block with matching ID
        
- Code is **scalable**: to add more tabs, just add more HTML — JS works automatically.
    

This is exactly what interviewers want.

---

# 🔥 Bonus: Add these improvements (highly scoring)

Try implementing each one to level up:

### ⭐ 1. Keyboard navigation

Left / Right arrows switch tabs.

### ⭐ 2. Default tab via URL hash

`#settings` loads Settings tab automatically.

### ⭐ 3. Animate content fade-in

Smooth transitions.

### ⭐ 4. Closeable tabs

Like browser tabs (dynamic create/remove).

### ⭐ 5. Vertical tabs mode

Tabs on the left, content on right.

### ⭐ 6. Reusable Class-Based Component

```
new TabsComponent(".tabs-container");
```

### ⭐ 7. Responsive scrollable tab bar

Auto horizontal scroll on overflow.

---

If you want, I can also give you:

🔸 Multi-tab UI with API content  
🔸 Tabs + Accordion combo  
🔸 Tabs with localStorage “remember last tab”  
🔸 A PDF-style _Machine Coding Round Problem Statement_  
🔸 A React version for deeper practice

Just tell me — I’ll prepare the next one!