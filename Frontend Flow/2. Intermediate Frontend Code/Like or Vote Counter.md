Great choice, Rahul!  
A **Like / Vote Counter** is a super common machine-coding round problem.  
It checks your skills in:

- DOM updates
    
- State management
    
- Event handling
    
- Component-like structure
    
- Edge cases (upvote/downvote toggle)
    

Let’s build a clean and interview-friendly project.

---

# 🚀 **Project: Post Like / Vote Counter Component**

You will build:

- A post card
    
- Like button
    
- Dislike button
    
- Vote count
    
- Toggle logic (cannot like & dislike at same time)
    
- Clean UI
    
- (Optional) Local Storage to persist likes
    

This is perfect for 20–40 minute machine coding rounds.

---

# 📁 **Folder Structure**

```
vote-counter/
│── index.html
│── style.css
└── script.js
```

---

# 🧱 **FULL WORKING PROJECT CODE**

---

## **index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vote Counter</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>

    <h1>Vote Counter - Machine Coding Round</h1>

    <div class="post-card">
        <p class="post-text">
            "This is a sample post. Click Like or Dislike to vote!"
        </p>

        <div class="actions">
            <button id="like-btn">👍 Like</button>
            <button id="dislike-btn">👎 Dislike</button>
        </div>

        <div class="count">
            Votes: <span id="vote-count">0</span>
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
    background: #f5f5f5;
    padding: 40px;
}

h1 {
    text-align: center;
    margin-bottom: 25px;
}

.post-card {
    background: white;
    padding: 20px;
    border-radius: 10px;
    max-width: 450px;
    margin: 0 auto;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

.post-text {
    font-size: 18px;
    margin-bottom: 20px;
}

.actions {
    display: flex;
    gap: 15px;
}

button {
    padding: 10px 18px;
    border: none;
    font-size: 16px;
    cursor: pointer;
    border-radius: 6px;
}

#like-btn.active {
    background: green;
    color: white;
}

#dislike-btn.active {
    background: red;
    color: white;
}

#vote-count {
    font-weight: bold;
    font-size: 20px;
}

.count {
    margin-top: 15px;
    text-align: center;
}
```

---

## **script.js**

```javascript
let voteCount = 0;
let liked = false;
let disliked = false;

const likeBtn = document.getElementById("like-btn");
const dislikeBtn = document.getElementById("dislike-btn");
const voteDisplay = document.getElementById("vote-count");

function updateDisplay() {
    voteDisplay.textContent = voteCount;
}

likeBtn.addEventListener("click", function () {
    if (liked) {
        // undo like
        liked = false;
        likeBtn.classList.remove("active");
        voteCount -= 1;
    } else {
        liked = true;
        likeBtn.classList.add("active");
        voteCount += 1;

        // remove dislike if active
        if (disliked) {
            disliked = false;
            dislikeBtn.classList.remove("active");
            voteCount += 1; // remove negative impact
        }
    }
    updateDisplay();
});

dislikeBtn.addEventListener("click", function () {
    if (disliked) {
        // undo dislike
        disliked = false;
        dislikeBtn.classList.remove("active");
        voteCount += 1; // removing -1
    } else {
        disliked = true;
        dislikeBtn.classList.add("active");
        voteCount -= 1;

        // remove like if active
        if (liked) {
            liked = false;
            likeBtn.classList.remove("active");
            voteCount -= 1; // removing +1
        }
    }
    updateDisplay();
});
```

---

# 🧠 **Logic Explanation (Interview Friendly)**

Say this to the interviewer:

- I maintain three states:  
    `voteCount`, `liked`, `disliked`.
    
- Clicking Like increases votes by +1.
    
- Clicking Dislike decreases votes by -1.
    
- If switching between like → dislike, I adjust voteCount correctly.
    
- UI button highlight uses `.active` class.
    
- Component behavior follows a toggle pattern.
    

Perfect, simple, clean.

---

# 🔥 **Upgrade Ideas (to impress interviewers)**

Want to stand out? Try these:

### ⭐ Componentized Version

Make it reusable:

```
new VoteComponent(containerId, initialCount)
```

### ⭐ Add “Total Likes” and “Total Dislikes” counters

Track separately.

### ⭐ Add Local Storage

Persist votes on page refresh.

### ⭐ Add multiple posts

Loop through posts array → create multiple vote components.

### ⭐ Keyboard support

Space = Like  
Backspace = Dislike

### ⭐ CSS animation for count bump

Smooth UI enhancement.

---

If you want, I can also give you:

💡 Multi-post version  
💡 Class-based component structure  
💡 React version  
💡 API version  
💡 Machine Coding Round PDF-style problem statement

Just tell me!