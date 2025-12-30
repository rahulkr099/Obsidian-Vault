Alright Rahul, let’s create a sharp and realistic **mock machine coding question** for **Search with Debounce**.  
This round checks your async thinking, UI updates, input handling, and performance — interviewers love this pattern.

---

# ✅ **Mock Interview Question — Search with Debounce (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 40 minutes

### **🎯 Goal:** Implement a **search box** that filters a list with **300ms debounce** and highlights matched text.

---

# **📝 Problem Statement**

You are given a list of items (strings).  
Your task is to build a **Search Component** with:

- A live search box
    
- **300ms debounce**
    
- Dynamic filtered results
    
- Matched text highlighting inside each result
    

Example input:

```js
const items = [
  "JavaScript Developer",
  "Frontend Engineer",
  "React Specialist",
  "Node.js Backend Developer",
  "Full Stack Engineer",
  "UI/UX Designer"
];
```

Your UI should include:

1. A search input field
    
2. A result list updated based on the search query
    
3. Highlighting the matching part of the result in bold or color
    

---

# **💡 Functional Requirements**

### **1️⃣ Debounced Search**

- User types → wait **300ms** before running the search.
    
- If user types again within those 300ms → reset timer.
    
- Should feel responsive and not laggy.
    

### **2️⃣ Dynamic Results**

- Show only items that match the search text.
    
- Case-insensitive search.
    
- If input is empty → show full list.
    

### **3️⃣ Highlight Matches**

- If query is “dev” and item is “JavaScript Developer”, highlight:
    
    ```
    JavaScript **Dev**eloper
    ```
    
- Highlights should not break for multiple occurrences.
    

### **4️⃣ Efficient Rendering**

- Avoid unnecessary re-renders.
    
- Handle fast typing smoothly.
    

### **5️⃣ Optional Keyboard Support**

- Arrow keys → move up/down through results
    
- Enter → select
    
- Escape → clear search
    

---

# **🧪 Edge Cases to Handle**

- **Empty search query** → return full original list.
    
- No matching items → show “No results found.”
    
- Query with spaces → trim input before filtering.
    
- Entering special characters → should not break highlight logic.
    
- Matching items that appear multiple times → highlight every match.
    
- Very large lists (e.g., 10,000+ items):
    
    - Debounce should prevent lag.
        
- If items update dynamically (API fetch):
    
    - Should re-run search cleanly.
        
- Continuous deletion (Backspace hold) → debounce should still work properly.
    

---

# **💬 Expected Output Behavior**

- Search feels lightweight and fast.
    
- Results update only after 300ms pause.
    
- Matching text is clearly marked.
    
- Smooth scrolling even for large lists.
    
- Clean UI layout.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you convert debounce into **throttle** and what’s the difference?
    
2. How would you handle **API-based search** with cancel tokens?
    
3. How would you highlight multiple matches in a string safely?
    
4. How would you optimize for extremely large lists (virtualization)?
    
5. How would you memoize search results?
    
6. How would you allow fuzzy search (Levenshtein distance)?
    

---

# 🌟 Innovative Ideas (Bonus to Impress)

- Add an animated loading indicator that appears during debounce.
    
- Add “clear search” (×) button inside the input.
    
- Add keyboard-accessible focus states in results.
    
- Add fuzzy search option (search even when words are slightly incorrect).
    
- Add suggestion highlighting (like Google autocomplete).
    
- Add grouping (e.g., group by job category or alphabetical).
    

---

If you want the next rounds — **Autocomplete**, **Virtualized List**, **Toast**, **Calendar**, **Infinite Scroll**, **Cart Component**, **Drag & Drop**, etc. — I can continue building the whole question bank for you!