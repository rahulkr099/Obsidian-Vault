Got you Rahul — here is a **top-quality, company-level mock interview question** on **Search + Debounce + Optimization**, which is one of the **most frequently asked machine coding patterns** in frontend interviews.

This includes:

✔ Real interview problem  
✔ Functional requirements  
✔ Edge cases  
✔ Failure scenarios  
✔ Acceptance criteria  
✔ Test cases  
✔ Bonus tasks

This is **exactly** the level of Swiggy, Meesho, Razorpay, PhonePe, Walmart, Amazon FE rounds.

Let’s build it properly.

---

# 🚀 **🔥 MACHINE CODING ROUND – Search Bar with Debounce + Keyboard Navigation**

## ⏱ Duration: 45–60 minutes

## 🧪 Difficulty: Medium

## 🧰 Tech: HTML + CSS + JavaScript (No frameworks)

---

# 📝 **📌 Problem Statement**

Build a **search component** that:

- Takes user input
    
- Runs search using **debounce (500ms)**
    
- Displays a filtered list below
    
- Shows **“No results found”** when applicable
    

Additionally, implement:

- Keyboard navigation: ↑ ↓ Enter
    
- (Optional) API-based search with GitHub Users API
    

---

# ✔️ **📋 Functional Requirements**

## 1️⃣ Search Input

- Text input field
    
- Start searching only after **500ms debounce**
    
- Search should trigger on typing AND on paste
    

## 2️⃣ Search Logic

- Filter from a given array (local list)
    
- Case-insensitive match
    
- Highlight the matching part (bonus)
    
- If no matches → show “No results found”
    

## 3️⃣ UI Behavior

- Show result list below input
    
- Each result is clickable
    
- Clicking a result fills the input
    

## 4️⃣ Keyboard Navigation (Important)

User should be able to:

- Press **ArrowDown (↓)** → move selection down
    
- Press **ArrowUp (↑)** → move selection up
    
- Press **Enter** → choose highlighted item
    

Rules:

- Wrap-around NOT required unless you choose
    
- Highlight item visually
    

## 5️⃣ API-based Search (Bonus)

Use GitHub API:

```
https://api.github.com/search/users?q=rahul
```

- Show username + avatar
    
- Apply same keyboard navigation
    
- Apply debounce to API calls
    

---

# ⚠️ **📌 Edge Cases (Critical — asked in interviews)**

### Input Edge Cases

- Empty input → clear results
    
- Input with only spaces → treat as empty
    
- Very fast typing → only last call should run
    
- Special characters → treat as normal search
    
- Input length = 1 → still allow search
    

### Result Edge Cases

- No match → show “No results found”
    
- Matching items > 100 → show max 10–20 (performance)
    
- Duplicate results → allow / dedupe (pick one and state it)
    

### Navigation Edge Cases

- Pressing arrow keys when list is empty → do nothing
    
- Pressing DOWN on last item → stay at last
    
- Pressing UP on first item → stay at first
    
- Press Enter without highlight → no action
    

### API Edge Cases (bonus)

- API rate limit hit (403)
    
- Slow network
    
- Empty query → don't call API
    
- Error response → show fallback message
    

---

# ❌ **📌 Failure Scenarios (Show interviewer you think deeply)**

- Debounce timer not cleared → multiple searches fire
    
- Memory leak → event listeners not cleaned
    
- Result list flickers if DOM recreated incorrectly
    
- Race condition: slower API response arrives after faster one
    
- API error → must handle gracefully
    
- Arrow key default browser behavior interfering
    
- No scroll support for many results
    

---

# 🎯 **📌 Acceptance Criteria (What counts as PASS)**

### UI:

- Clean, compact search dropdown
    
- Smooth highlight transitions
    
- Selected result visually distinct
    
- “No results found” styled nicely
    

### Behavior:

- Debounce EXACTLY 500ms
    
- Zero lag while typing
    
- Arrow key navigation smooth
    
- Clicking result fills input
    
- Enter key works even without mouse
    
- No unnecessary re-render
    
- Works on both desktop + mobile
    

### Code:

- Standalone **debounce()** function
    
- Separate functions:
    
    - performSearch
        
    - renderResults
        
    - handleKeyboard
        
- No inline event handlers
    
- No global variable pollution
    
- Clean naming
    
- No console errors
    

---

# 🧪 **📌 Test Cases**

|Action|Expected Output|
|---|---|
|Type “ra”|Show all items containing "ra"|
|Type “rahul”|Show matching items OR “No results found”|
|Clear input|Clear results immediately|
|Press ↓ twice|Highlight 2nd item|
|Press ↑ at top|Highlight stays at top|
|Press Enter|Input filled with highlighted item|
|Click on result|Input filled with clicked text|
|Fast typing “rahul”|Only ONE final search runs|
|Paste text|Debounce should trigger|
|API offline|Show “Something went wrong”|
|API returned empty|“No users found”|

---

# ⭐ **📌 Bonus (Optional – adds extra points)**

- Highlight matching text
    
- Loading indicator
    
- Keyboard shortcut: ESC to close results
    
- Scroll when many results are present
    
- Fuzzy search instead of substring search
    
- Keep search history in localStorage
    
- Show avatars (for GitHub API)
    
- Dark mode
    

---

# 🎤 **📌 Interviewer Evaluation Guide**

They will check:

### Logic

- Correct debounce usage
    
- Efficient search
    
- No flickering
    
- Clean navigation logic
    

### UI

- Smooth transitions
    
- Good accessibility
    
- Keyboard-friendly
    

### Code

- Modular, readable functions
    
- Good variable naming
    
- No repeated logic
    
- Edge cases handled gracefully
    

### Attitude

- Calmness
    
- Ability to explain
    
- No overengineering
    

---

# Rahul — this is EXACTLY how real FE machine coding rounds present **Search Components**.

If you want next:

👉 **Start this mock round**  
👉 **Give me full working solution**  
👉 **Give me API version solution**  
👉 **Give me React version**  
👉 **Give me a UI mockup template**

Just say the word — I’m here with you.