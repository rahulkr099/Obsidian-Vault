Alright Rahul, here comes a polished and interview-realistic **mock machine coding round question** for a **Shopping Cart Component**.  
This round checks your ability to manage complex state, compute totals, handle UI updates, and cover edge cases — exactly what interviewers love.

---

# ✅ **Mock Interview Question — Shopping Cart (Frontend Machine Coding Round)**

### **⏱ Time Limit:** 45 minutes

### **🎯 Goal:** Build a **Shopping Cart system** where users can add items, remove items, update quantity, and view totals.

---

# **📝 Problem Statement**

You are given a list of products.  
You must build a **shopping cart UI** that allows:

- Adding items to cart
    
- Removing items
    
- Updating item quantity
    
- Showing item-level totals
    
- Showing overall cart total
    

Sample products:

```js
const products = [
  { id: 1, name: "Wireless Mouse", price: 599 },
  { id: 2, name: "Mechanical Keyboard", price: 2499 },
  { id: 3, name: "USB-C Cable", price: 199 }
];
```

You must build:

1. A **product list** with an “Add to Cart” button.
    
2. A **cart section** that updates dynamically.
    
3. A **clean and readable UI** showing all calculations.
    

---

# **💡 Functional Requirements**

### **1️⃣ Add to Cart**

- Clicking “Add to Cart”:
    
    - If item is **not** in cart → add it with quantity = 1.
        
    - If item is already in cart → increase its quantity by 1.
        

### **2️⃣ Update Quantity**

- In the cart, each item should have:
    
    - `+` button → increase quantity
        
    - `–` button → decrease quantity
        
    - Quantity cannot go below 1
        

### **3️⃣ Remove Item**

- Add a “Remove” or “Delete” button.
    
- Removing an item should:
    
    - Remove it from the cart completely
        
    - Update total immediately
        

### **4️⃣ Price Calculation**

For each cart item:

```
Item Total = price * quantity
```

For the entire cart:

```
Cart Total = sum of all item totals
```

### **5️⃣ Clean UI**

- Items must be easy to scan.
    
- Totals should be visible and always up-to-date.
    
- Mobile layout should look clean too.
    

### **6️⃣ State Consistency**

- No duplicate items.
    
- Quantity updates should not break totals.
    
- Should handle rapid clicking correctly.
    

---

# **🧪 Edge Cases to Handle**

- Adding same item repeatedly → quantity increases, no duplicates.
    
- Removing an item while clicking increment/decrement fast → no UI crash.
    
- Cart becomes empty → show “Cart is empty”.
    
- Prices might be `0` → UI shouldn’t break.
    
- Very large quantities (e.g., user clicks + 100 times) → still stable.
    
- Item removed while cart total is 0 should not cause negative totals.
    
- If product list updates externally (API) → cart must still work cleanly.
    
- Quick add/remove must not overshoot quantity or totals.
    

---

# **💬 Expected Output Behavior**

- Cart updates instantly.
    
- Totals recalculate immediately when quantity changes.
    
- Removing items works smoothly.
    
- Layout remains clean and readable.
    

---

# ⭐ Interviewer Follow-Up Questions

1. How would you sync cart data to **localStorage** so it persists after reload?
    
2. How would you handle API calls for cart updates (add/remove)?
    
3. How would you make a reusable `useCart()` hook?
    
4. How would you prevent performance issues with large carts (e.g., 200 items)?
    
5. How would you show a confirmation modal before removing an item?
    
6. How would you debounce quantity changes before syncing with server?
    

---

# 🌟 Innovative Ideas (Bonus to Impress)

- Add a mini-cart popup (like Amazon’s top-right cart).
    
- Add discount coupon logic.
    
- Add stock limit validation (e.g., max 5 items).
    
- Add animation when adding items to cart (item flies to cart).
    
- Add undo “Removed item” feature.
    
- Add subtotal / tax / shipping section.
    
- Add persistence using:
    
    - localStorage
        
    - IndexedDB
        
    - URL cart state
        

---

If you want, we can move to:

➡️ **Round 12 — Toast Notification**  
➡️ **Round 13 — File Upload**  
➡️ **Round 14 — Infinite Scroll**  
➡️ **Round 15 — Virtualized List**

Just tell me — I’ll prepare the next one for you!