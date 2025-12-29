Alright Rahul, let’s build a **clean, interview-friendly Accordion Component** using pure **HTML, CSS, and JavaScript** — exactly like machine-coding rounds.

This problem checks:

- DOM manipulation
    
- Event handling
    
- Toggling logic
    
- Reusable components
    
- Clean, readable code
    

I’ll give you:

✅ Problem statement  
✅ Full working code (HTML + CSS + JS)  
✅ One-open-at-a-time accordion  
✅ Smooth animation  
✅ Bonus improvements to level up

Let’s start!

---

# 🚀 **Machine Coding Round Project: Accordion Component**

---

## 📌 **Problem Statement (Interviewer Style)**

Build an **Accordion** UI that:

- Displays multiple accordion items (question → answer).
    
- Clicking a header should **toggle** its content.
    
- Only one accordion item should be open at a time.
    
- Smooth open/close animation.
    
- Clean, modular structure.
    

---

# 🧱 **FULL WORKING PROJECT**

---

## **index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Accordion Component</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>

<h1>Accordion Component (Machine Coding Round)</h1>

<div class="accordion">

    <div class="accordion-item">
        <div class="accordion-header">What is JavaScript?</div>
        <div class="accordion-body">
            JavaScript is a programming language used to build interactive web apps.
        </div>
    </div>

    <div class="accordion-item">
        <div class="accordion-header">What is an Accordion?</div>
        <div class="accordion-body">
            An accordion is a UI component that expands and collapses sections.
        </div>
    </div>

    <div class="accordion-item">
        <div class="accordion-header">Why is it used?</div>
        <div class="accordion-body">
            Accordions help organize large amounts of content into small spaces.
        </div>
    </div>

</div>

<script src="script.js"></script>
</body>
</html>
```

---

## **style.css**

```css
body {
    font-family: Arial, sans-serif;
    background: #f7f7f7;
    padding: 40px;
}

h1 {
    text-align: center;
    margin-bottom: 25px;
}

.accordion {
    max-width: 600px;
    margin: 0 auto;
}

.accordion-item {
    background: white;
    margin-bottom: 10px;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

.accordion-header {
    padding: 15px;
    background: #eee;
    cursor: pointer;
    font-size: 17px;
}

.accordion-body {
    max-height: 0;
    overflow: hidden;
    background: white;
    padding: 0 15px;
    font-size: 16px;
    transition: max-height 0.3s ease, padding 0.3s ease;
}

.accordion-item.active .accordion-body {
    padding: 15px;
}
```

---

## **script.js**

```javascript
const items = document.querySelectorAll(".accordion-item");

items.forEach(item => {
    const header = item.querySelector(".accordion-header");

    header.addEventListener("click", () => {
        
        // Close all
        items.forEach(i => {
            if (i !== item) {
                i.classList.remove("active");
                i.querySelector(".accordion-body").style.maxHeight = null;
            }
        });

        // Toggle clicked one
        item.classList.toggle("active");

        const body = item.querySelector(".accordion-body");

        if (item.classList.contains("active")) {
            body.style.maxHeight = body.scrollHeight + "px";
        } else {
            body.style.maxHeight = null;
        }
    });
});
```

---

# 🎯 **How You Can Explain This in an Interview**

Use this explanation; it's crisp and professional:

- Each accordion item has a header + body.
    
- I attach click listeners to all headers.
    
- When a header is clicked:
    
    - I close all other accordion items.
        
    - Then toggle only the clicked one.
        
- Animations are done using `max-height` CSS transitions.
    
- `scrollHeight` gives the real height of content, allowing smooth expansion.
    
- This structure is scalable — adding more items does not need more JS.
    

Perfect interview answer.

---

# 🔥 Extra Features to Practice (Highly Recommended)

Try adding these one by one:

### ⭐ 1. **Multiple items open at once** (optional mode)

Toggle between single-open vs multi-open.

### ⭐ 2. **Arrow icon rotation**

Rotate a chevron when expanded.

### ⭐ 3. **Keyboard navigation**

Arrow ↑↓ to move, Enter to open.

### ⭐ 4. **ARIA roles for accessibility**

Add:

```
role="button"
aria-expanded="false"
```

### ⭐ 5. **Dark theme toggle**

### ⭐ 6. Reusable class:

```
new Accordion('.accordion');
```

### ⭐ 7. Dynamic accordion (data-driven)

Generate items from an array.

---

If you want, I can also give you:

📘 Accordion + Tabs combo  
📘 Accordion with search/filter  
📘 Accordion for FAQs (real project)  
📘 A PDF-style “Machine Coding Round” problem statement

Just tell me — I’ll build the next one!