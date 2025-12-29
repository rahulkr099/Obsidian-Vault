Perfect, Rahul!  
A **Modal Component** is a classic machine-coding round question.  
It tests:

- DOM manipulation
    
- Event delegation
    
- Overlay handling
    
- Accessibility basics
    
- Animation
    
- Reusable component design
    

I’ll give you:

✅ Interview-style problem statement  
✅ Full working HTML + CSS + JS  
✅ Close on button click, outside click, and ESC key  
✅ Smooth fade animation  
✅ Clean, scalable structure  
✅ Bonus enhancements to master the pattern

Let’s build it!

---

# 🚀 **Machine Coding Round Project: Modal Component**

---

## 📌 **Problem Statement (Interviewer Style)**

Build a **Modal Popup Component** with the following features:

- A button opens the modal
    
- Modal appears in the center with an overlay
    
- Modal closes when:  
    ✔ user clicks the close button  
    ✔ user clicks outside the modal  
    ✔ user presses the ESC key
    
- Modal should have smooth fade-in / fade-out animation
    
- Structure should allow creating more modals easily
    

---

# 🧱 **FULL WORKING PROJECT**

---

# 📂 **index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Modal Component</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>

    <h1>Modal Component (Machine Coding Round)</h1>

    <button id="open-modal" class="open-btn">Open Modal</button>

    <!-- Overlay -->
    <div id="overlay" class="overlay"></div>

    <!-- Modal -->
    <div id="modal" class="modal">
        <div class="modal-header">
            <h2>Modal Title</h2>
            <button id="close-modal" class="close-btn">✖</button>
        </div>
        <div class="modal-body">
            This is the content inside the modal.
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
```

---

# 📂 **style.css**

```css
body {
    font-family: Arial, sans-serif;
    padding: 40px;
    background: #f5f5f5;
}

h1 {
    text-align: center;
    margin-bottom: 25px;
}

.open-btn {
    padding: 12px 20px;
    background: black;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    display: block;
    margin: 0 auto;
}

/* Modal Overlay */
.overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.6);
    opacity: 0;
    pointer-events: none;
    transition: 0.3s ease;
}

/* Modal Box */
.modal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -60%);
    background: white;
    width: 400px;
    padding: 20px;
    border-radius: 10px;
    opacity: 0;
    pointer-events: none;
    transition: 0.3s ease;
    box-shadow: 0 8px 20px rgba(0,0,0,0.15);
}

/* Active State */
.overlay.active {
    opacity: 1;
    pointer-events: all;
}

.modal.active {
    opacity: 1;
    pointer-events: all;
    transform: translate(-50%, -50%);
}

/* Header */
.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.close-btn {
    background: red;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    padding: 5px 10px;
}
```

---

# 📂 **script.js**

```javascript
const openBtn = document.getElementById("open-modal");
const closeBtn = document.getElementById("close-modal");
const modal = document.getElementById("modal");
const overlay = document.getElementById("overlay");

// Open modal
function openModal() {
    modal.classList.add("active");
    overlay.classList.add("active");
}

// Close modal
function closeModal() {
    modal.classList.remove("active");
    overlay.classList.remove("active");
}

// Button click
openBtn.addEventListener("click", openModal);
closeBtn.addEventListener("click", closeModal);

// Click outside modal
overlay.addEventListener("click", closeModal);

// Close on ESC key
document.addEventListener("keydown", (e) => {
    if (e.key === "Escape") closeModal();
});
```

---

# 🎯 **Interview Explanation You Can Give**

You can answer like this:

- Modal is hidden using `opacity: 0` and `pointer-events: none`
    
- When opened, I toggle an `.active` class
    
- This enables smooth transitions using CSS
    
- Overlay prevents interaction with background
    
- Modal closes on:
    
    - Close button click
        
    - Outside click (overlay)
        
    - ESC key
        
- Logic is modular, so multiple modals can reuse the same functions
    

Interviewer will love this structure.

---

# 🔥 **Bonus Features to Level Up**

If you want to master modals, try adding these:

### ⭐ 1. Center modal with resize handling

Auto-center even on window resize.

### ⭐ 2. Multiple modals

Trigger different content using:

```
data-modal="info"
data-modal="warning"
```

### ⭐ 3. Focus trap

Keep keyboard focus inside the modal for accessibility.

### ⭐ 4. Animation (scale-in, slide-in, fade-in)

### ⭐ 5. Prevent background scroll

Add/remove:

```
document.body.style.overflow = "hidden";
```

### ⭐ 6. “Modal Manager” class

Reusable component:

```
new Modal('#modal');
```

### ⭐ 7. Dynamic content

Pass content programmatically:

```
openModal("User details loaded from API...");
```

---

If you want, I can also prepare:

📘 Machine Coding PDF  
📘 Modal + Form validation  
📘 Modal + Shopping cart checkout  
📘 React version of modal

Just tell me — I’ll make the next one!