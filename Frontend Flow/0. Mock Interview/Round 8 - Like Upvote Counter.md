Alright Rahul, here comes a clean and interview-ready **mock machine coding round question** for a **Like / Upvote Counter**.  
This one is simple on the surface but interviewers use it to check your state management skills, edge-case handling, and clean thinking.

---

# ✅ **Mock Interview Question — Like / Upvote Counter (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 30 minutes

### **🎯 Goal:** Build an **upvote/downvote toggle system** with a live counter.

---

# **📝 Problem Statement**

Create a **Like / Dislike counter component** that allows users to:

- Upvote
    
- Downvote
    
- Remove their vote
    
- Maintain correct vote count
    

The rule:

👉 **User cannot like and dislike at the same time.**

You will be given:

```js
const initialLikes = 120;
const initialDislikes = 10;
```

Show the two buttons and counters beside them.

---

# **💡 Functional Requirements**

### **1️⃣ Toggle Rules**

- Clicking **Upvote**:
    
    - If not already upvoted → upvote count +1
        
    - If already upvoted → remove upvote (count -1)
        
    - If previously downvoted → remove downvote (count -1), then add upvote (+1)
        
- Clicking **Downvote**:
    
    - If not already downvoted → downvote count +1
        
    - If already downvoted → remove downvote
        
    - If previously upvoted → remove upvote (count -1), then add downvote (+1)
        

### **2️⃣ Visual Highlight**

- Active button should be highlighted (color or filled icon).
    
- Inactive button should stay normal.
    

### **3️⃣ Clean UI**

- Numbers must update instantly.
    
- Buttons must feel responsive.
    
- Layout should work well on mobile too.
    

---

# **🧪 Edge Cases to Cover**

- User toggles rapidly between upvote ↔ downvote → counts should never misalign.
    
- User clicks upvote multiple times fast → must not double increment.
    
- Initial likes/dislikes may be `0`, component should still work.
    
- Count numbers may become large → should not overflow layout.
    
- Clicking inside buttons should not propagate and break UI.
    
- If data updates externally (like from server), the UI should re-sync.
    

---

# **💬 Expected Output Behavior**

- Clicking upvote once increases number and highlights the icon.
    
- Clicking again removes it.
    
- Switching from upvote to downvote should adjust both counts correctly.
    
- Smooth and instant UI updates.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you sync this with a backend API?
    
2. How would you prevent double updates during network delay?
    
3. How would you handle optimistic UI updates vs. actual server result?
    
4. How would you animate the count (bounce effect)?
    
5. How would you handle thousands of votes efficiently?
    

---

# 🌟 Innovative Ideas (Good for Impressing Interviewers)

- Add a small animation on clicking (scale pop).
    
- Add a tooltip “You liked this”.
    
- Add keyboard shortcuts for upvote/downvote.
    
- Add API retry mechanism.
    
- Add long-press support (mobile friendly).
    
- Add event batch updates (for real-time server sync).
    

---

Want to continue to **Round 9 — File Upload**, **Round 10 — Toast Notification**, **Round 11 — Virtual List**, **Round 12 — Carousel**, or **Backend rounds**?  
I’m happy to keep building your full interview bank!