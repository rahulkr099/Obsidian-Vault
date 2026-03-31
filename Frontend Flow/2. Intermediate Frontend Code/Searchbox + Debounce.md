Got you Rahul! Let’s build a clean **Search Box + Debounce** project — exactly the type that comes in machine coding rounds.

I'll give you:

✅ Clear problem statement (interview-style)  
✅ Required features  
✅ Full HTML + CSS + JS code  
✅ Dummy data  
✅ Debounce implemented from scratch  
✅ Extra improvement ideas to level up your solution

Let's go!

---

# 🚀 **Machine Coding Round Project: Search Box with Debounce**

This is a classic interview question to test:

- DOM manipulation
    
- Event handling
    
- Debouncing
    
- Search logic efficiency
    
- Clean UI
    
- Code structure
    

Perfect for FAANG-style rounds.

---

# 📌 **1. Requirements (as per interview format)**

**You must build:**

- A search input box.
    
- As the user types, search suggestions should appear.
    
- Use **debounce** (300ms).
    
- Highlight matching text.
    
- Clean UI.
    
- Click on a suggestion → show it selected.
    

---

# 📁 **2. Folder Structure**

```
search-debounce/
│── index.html
│── style.css
└── script.js
```

---

# 🧱 **3. FULL WORKING CODE**

---

## **index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Search Box with Debounce</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>

    <h2>Search Users</h2>

    <input type="text" id="search-input" placeholder="Search something..." />

    <div id="results"></div>

    <script src="script.js"></script>
</body>
</html>
```

---

## **style.css**

```css
body {
  font-family: Arial, sans-serif;
  padding: 30px;
  background: #f7f7f7;
}

#search-input {
  width: 100%;
  padding: 12px;
  font-size: 16px;
  border: 2px solid #ddd;
  border-radius: 6px;
}

#results {
  margin-top: 15px;
  background: #fff;
  border-radius: 6px;
  overflow: hidden;
}

.result-item {
  padding: 12px;
  border-bottom: 1px solid #eee;
  cursor: pointer;
}

.result-item:hover {
  background: #fafafa;
}

.highlight {
  background: yellow;
  font-weight: bold;
}
```

---

## **script.js**

```javascript
// Dummy Data
const users = [
  "Rahul Kumar",
  "Aman Sharma",
  "Rishabh Sen",
  "Sneha Kapoor",
  "Aditya Singh",
  "Rohan Das",
  "Neha Verma",
  "Arjun Rao",
  "Ananya Roy",
  "Priya Mehta",
  "Aniket Joshi",
  "Aarav Patel"
];

const searchInput = document.getElementById("search-input");
const resultsContainer = document.getElementById("results");

// Debounce function
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

// Search function
function searchUsers(query) {
  resultsContainer.innerHTML = "";

  if (!query.trim()) return;

  const lowerQuery = query.toLowerCase();

  const filtered = users.filter(user =>
    user.toLowerCase().includes(lowerQuery)
  );

  filtered.forEach(user => {
    const item = document.createElement("div");
    item.classList.add("result-item");

    // Highlight match
    const regex = new RegExp(`(${lowerQuery})`, "gi");
    const highlighted = user.replace(regex, `<span class="highlight">$1</span>`);

    item.innerHTML = highlighted;
    item.onclick = () => {
      searchInput.value = user;
      resultsContainer.innerHTML = "";
    };

    resultsContainer.appendChild(item);
  });
}

// Debounced version
const debouncedSearch = debounce(() => {
  const query = searchInput.value;
  searchUsers(query);
}, 300);

// Input listener
searchInput.addEventListener("input", debouncedSearch);
```

---

# 🎯 **4. How it works**

- As user types → event triggers.
    
- But actual search runs only after **300ms** of pause.
    
- Search matches with dummy user list.
    
- Output renders suggestions.
    
- Matching text is highlighted yellow.
    
- Clicking suggestion fills input.
    

All these are exactly what interviewers check.

---

# 🔥 **5. Bonus: Add these to impress interviewers**

You can improve it with:

### ⭐ API Search Mode

Instead of dummy list, fetch from API with debounce:

```
https://dummyjson.com/users/search?q=
```

### ⭐ Keyboard navigation

Up ↑ / Down ↓ to select items.

### ⭐ Recent search history

Store in localStorage.

### ⭐ Clear search (X button)

### ⭐ Loading indicator

Show spinner while waiting for debounce.

---

If you want, I can give you:

✅ API-based version  
✅ Debounce + Throttle combined version  
✅ Search with images (like GitHub users)  
✅ TypeScript version  
✅ Machine coding round problem PDF style

Just tell me!