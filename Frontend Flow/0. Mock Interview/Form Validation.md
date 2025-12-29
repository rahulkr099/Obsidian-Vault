Alright Rahul — here is a **complete, industry-standard mock machine coding round question** on **Real-Time Form Validation**, written exactly like product companies ask.

This includes:

✔ Problem statement  
✔ Functional requirements  
✔ Frontend rules  
✔ Validation rules  
✔ Edge cases  
✔ Failure scenarios  
✔ Acceptance criteria  
✔ Test cases  
✔ Bonus tasks (optional)

This is **perfect for practicing UI + validation logic**, which is a REAL machine coding favorite.

Let’s begin.

---

# 🚀 **FULL MOCK MACHINE CODING ROUND – Real-Time Registration Form Validation**

## ⏱ **Duration:** 45 minutes

## 🧪 **Difficulty:** Easy–Medium

## ⚙ **Tech:** HTML, CSS, JavaScript (no frameworks)

---

# 📝 **📌 Problem Statement**

Build a **registration form with real-time validation**, where:

- Validation happens **while typing**
    
- Errors appear **inline** under each field
    
- The **Submit** button remains disabled until **all fields are valid**
    
- Password shows a **strength meter** (weak → medium → strong)
    

This is the **exact kind of question** asked in:

- Swiggy
    
- Zomato
    
- Meesho
    
- Razorpay
    
- Walmart
    
- Freshworks
    
- Startups
    

---

# 🧩 **📋 Functional Requirements**

### ✔ 1. Fields:

- Username
    
- Email
    
- Password
    
- Submit button
    

### ✔ 2. Real-time validation

- When typing inside any field → run validation
    
- Error messages should update instantly
    
- Submit button should activate only when **all fields are valid**
    

### ✔ 3. Inline errors

Each field must show an error below it:

```
Username is required  
Invalid email  
Password too weak  
```

### ✔ 4. Password strength indicator

Show strength as:

- Weak → Red
    
- Medium → Orange
    
- Strong → Green
    

Based on:

- Length
    
- Special chars
    
- Numbers
    
- Uppercase
    

### ✔ 5. On successful submit

Show:

```
Registration Successful
```

(no backend required)

---

# 📐 **📌 Validation Rules**

### Username:

- Required
    
- Minimum 3 chars
    
- Only letters, numbers, underscores allowed
    
- No spaces
    

### Email:

- Required
    
- Must follow email pattern (basic regex ok)
    

### Password:

- Required
    
- Minimum 6 chars
    
- Must include:
    
    - 1 uppercase
        
    - 1 number
        
    - 1 special character (@#$%^&*!?)
        

### Submit button:

- Disabled until all fields valid
    

---

# ⚠️ **📌 Edge Cases**

These are critical — interviewers check this part!

### Username:

- Starts with a number → ❌ invalid
    
- Contains space → ❌ invalid
    
- Two underscores in a row → ❌ invalid
    
- Empty input → show error as soon as they blur the field
    

### Email:

- “abc@” → invalid
    
- Missing domain → invalid
    
- Extra spaces before/after → trim input
    
- Email in uppercase is still valid (“[RAHUL@GMAIL.COM](mailto:RAHUL@GMAIL.COM)”)
    

### Password:

- Only numbers → ❌ invalid
    
- Only letters → ❌ invalid
    
- Contains space → ❌ invalid
    
- Entering extremely long passwords → accept but handle smoothly
    

### General:

- User clears field → show error immediately
    
- Submit clicked while invalid → do nothing
    
- Pasting values should also trigger validation
    

---

# 💥 **📌 Failure Scenarios (Interviewers LOVE when you consider these)**

- JavaScript disabled → form will not work (acceptable)
    
- User pastes invalid email → must validate
    
- Slow typing / fast typing → debounce NOT required
    
- Multiple errors should not overlap
    
- Error message should not flicker
    
- Strength meter should not misclassify password
    
- Form must NOT submit if:
    
    - Any field is empty
        
    - Any field invalid
        
    - Errors exist
        

---

# 🧪 **📌 Test Cases (very important)**

|Input|Expected Result|
|---|---|
|Username: “ra”|❌ error: min 3 chars|
|Username: “rahul_k”|✔ valid|
|Email: “rahul@”|❌ invalid email|
|Email: “[rahul@gmail.com](mailto:rahul@gmail.com)”|✔ valid|
|Password: “abc”|❌ weak, show error|
|Password: “Abc123”|✔ medium|
|Password: “Abc@12345”|✔ strong|
|All fields valid|Submit enabled|
|Clear a valid field|Submit disabled again|

---

# 🎯 **📌 Acceptance Criteria**

To pass the interview, your solution MUST:

### UI:

- Clean and readable
    
- Error messages clear and not too big
    
- Strength meter visually obvious
    
- Submit disabled by default
    

### Code:

- No duplicated logic
    
- Separate validation functions
    
- Readable variable names
    
- No inline JS
    
- No console errors
    
- No global namespace pollution
    

### Behavior:

- Realtime feedback
    
- Smooth error updates
    
- Button enable/disable reliable
    
- Strength meter accurate
    

---

# ⭐ **Bonus (if time allows — adds extra points!)**

- Show small icons (✔ / ✖) next to inputs
    
- Add show/hide password toggle
    
- Add “confirm password” field
    
- Add simple animations for errors
    
- Save partially typed input in localStorage
    
- Add dark mode
    

---

# Rahul, this is EXACTLY how real frontend machine coding rounds are written.

If you want, I can now:

👉 Generate the **solution**  
👉 Start a **live mock round** and evaluate your code  
👉 Provide a **starter template**  
👉 Create the **backend version** of this form  
👉 Add **more UI/UX variations**

Just tell me:  
**“Start this mock round”** or  
**“Give me the solution”**