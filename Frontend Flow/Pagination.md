Alright Rahul, let’s build a neat little **pagination machine-coding practice project** using pure **HTML, CSS, and JavaScript**.  
I’ll give you:

✅ Project idea  
✅ Features you should implement  
✅ Starter UI  
✅ Complete working code  
✅ Extra improvements to try (for interview “wow factor”)

Let’s jump in!

---

# 🚀 **Project: User List Pagination (Machine Coding Round Style)**

This is a classic interview-style problem — you get data, show items per page, and allow switching between pages.

---

# ✅ **1. Project Requirements (as in interviews)**

**You must implement:**

- Show a list of **dummy users** (50–100).
    
- Show **10 users per page**.
    
- Create **Next**, **Previous**, and **numbered page buttons**.
    
- Highlight the **current** page.
    
- Disable buttons when needed.
    
- Clean UI (simple CSS).
    

---

# 📁 **2. Folder Structure**

```
pagination-project/
│── index.html
│── style.css
└── script.js
```

---

# 🧱 **3. FULL WORKING CODE**

(You can copy–paste and run)

---

## **index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pagination Project</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>
    <h1>User List with Pagination</h1>

    <div id="user-container"></div>

    <div id="pagination"></div>

    <script src="script.js"></script>
</body>
</html>
```

---

## **style.css**

```css
body {
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  padding: 30px;
}

#user-container {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
}

.user-item {
  padding: 12px;
  border-bottom: 1px solid #eee;
}

#pagination {
  display: flex;
  gap: 10px;
  justify-content: center;
}

button {
  padding: 8px 14px;
  border: none;
  background: #ddd;
  border-radius: 5px;
  cursor: pointer;
}

button.active {
  background: black;
  color: white;
}

button:disabled {
  background: #aaa;
  cursor: not-allowed;
}
```

---

## **script.js**

```javascript
// Dummy user data
const users = Array.from({ length: 50 }, (_, i) => `User ${i + 1}`);

const userContainer = document.getElementById("user-container");
const pagination = document.getElementById("pagination");

let currentPage = 1;
const usersPerPage = 10;

// Render users of the page
function renderUsers(page) {
  userContainer.innerHTML = "";

  const start = (page - 1) * usersPerPage;
  const end = start + usersPerPage;

  users.slice(start, end).forEach((user) => {
    const div = document.createElement("div");
    div.classList.add("user-item");
    div.textContent = user;
    userContainer.appendChild(div);
  });
}

// Render pagination buttons
function renderPagination() {
  pagination.innerHTML = "";

  const totalPages = Math.ceil(users.length / usersPerPage);

  // Previous button
  const prevBtn = document.createElement("button");
  prevBtn.textContent = "Prev";
  prevBtn.disabled = currentPage === 1;
  prevBtn.onclick = () => changePage(currentPage - 1);
  pagination.appendChild(prevBtn);

  // Numbered pages
  for (let i = 1; i <= totalPages; i++) {
    const btn = document.createElement("button");
    btn.textContent = i;
    if (i === currentPage) btn.classList.add("active");
    btn.onclick = () => changePage(i);
    pagination.appendChild(btn);
  }

  // Next button
  const nextBtn = document.createElement("button");
  nextBtn.textContent = "Next";
  nextBtn.disabled = currentPage === totalPages;
  nextBtn.onclick = () => changePage(currentPage + 1);
  pagination.appendChild(nextBtn);
}

function changePage(page) {
  currentPage = page;
  renderUsers(page);
  renderPagination();
}

// initialize
changePage(1);
```

---

# 🌱 **4. Extra Features (Interview Value Boosters)**

Here are some cool additions to impress interviewers:

### ⭐ **(1) Add “Go to Page” input**

User can type page number → jump to that screen.

### ⭐ **(2) Add dropdown: “Items per page”**

5 / 10 / 20 / 50 per page.

### ⭐ **(3) Fetch live data**

Use JSONPlaceholder API:

```js
fetch("https://jsonplaceholder.typicode.com/users")
```

### ⭐ **(4) Add animations**

Fade in items while switching pages.

### ⭐ **(5) Add search filter**

Search users + pagination together.

---

# 🔥 If you want, I can also give:

✅ A version using **cards UI**  
✅ A version using **fetch API**  
✅ A version with **server-side pagination simulation**  
✅ A **DSA-style approach** explanation for pagination logic

Just tell me — I’ll build the next level for you!