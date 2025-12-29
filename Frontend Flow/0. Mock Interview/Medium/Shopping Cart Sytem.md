Alright Rahul — here is a **top-quality, company-level mock interview question** for a **Shopping Cart System**, one of the MOST COMMON frontend + logic machine coding rounds.

This version includes:

✔ Functional requirements  
✔ Data-handling rules  
✔ UI expectations  
✔ Edge cases  
✔ Failure scenarios  
✔ Acceptance criteria  
✔ Test cases  
✔ Bonus logic (discounts + tax)

This is the EXACT style used at:

**Swiggy, Meesho, Flipkart, Amazon, Razorpay, PhonePe, Zomato, Hotstar, Startups**

Let’s make it crystal clear and interview-ready.

---

# 🚀 **🔥 MACHINE CODING ROUND – Shopping Cart System**

## ⏱ Duration: 45–60 minutes

## 🧪 Difficulty: Medium

## 🧰 Tech: HTML + CSS + JavaScript (No frameworks)

---

# 📝 **📌 Problem Statement**

Build a **Shopping Cart** UI that:

- Shows a list of products
    
- Allows adding products to cart
    
- Allows removing items from cart
    
- Allows increasing/decreasing quantity
    
- Calculates total price dynamically
    

Extra (Bonus):

- Apply discount coupons
    
- Show final price after tax
    

---

# 📦 **📋 Data (Static Product List)**

Example structure:

```js
[
  { id: 1, name: "Laptop", price: 50000 },
  { id: 2, name: "Headphones", price: 2000 },
  { id: 3, name: "Keyboard", price: 1500 }
]
```

---

# 🧩 **📋 Functional Requirements**

## ⭐ 1️⃣ Show Product List

- Display product name + price
    
- Each product should have an **“Add to Cart”** button
    
- When clicked:
    
    - If item already in cart → increase qty by 1
        
    - Else → add item with qty = 1
        

---

## ⭐ 2️⃣ Cart Section

Each cart item must display:

- Product name
    
- Price
    
- Quantity input or +/- buttons
    
- Remove button
    
- Subtotal (price * qty)
    

---

## ⭐ 3️⃣ Update Quantity

- Clicking **+** increases qty
    
- Clicking **−** decreases qty
    
- Qty cannot go below **1**
    
- Subtotal updates instantly
    
- Total updates instantly
    

---

## ⭐ 4️⃣ Remove from Cart

- Remove button deletes the item completely
    
- Total updates instantly
    
- If cart is empty → show “Cart is Empty”
    

---

## ⭐ 5️⃣ Total Price Calculation

Total = Sum of subtotal of all cart items

Update total:

- On add
    
- On delete
    
- On qty update
    

---

# 💡 **💰 Extra (Bonus Features)**

## 1️⃣ Discount Coupon Logic

Coupons example:

- `SAVE10` → 10% off
    
- `FLAT200` → deduct ₹200
    

Rules:

- Coupon should apply only once
    
- Invalid coupon → show error
    
- Show final discounted price
    

---

## 2️⃣ Tax Calculation

Add 18% GST (or configurable)

Final = (total - discount) + tax

---

# ⚠️ **📌 Edge Cases (Critical for interviews)**

### Cart Behavior

- Adding same product twice → increase qty, do NOT duplicate row
    
- Qty cannot exceed a maximum limit (say 10 or configurable)
    
- Qty cannot go below 1
    
- Removing item while qty > 1 → allowed
    

### Prices

- Floating price calculations → round to 2 decimal places
    
- Zero price products (rare) → handle properly
    

### Discount

- Entering coupon with spaces → trim input
    
- Applying coupon twice → allow once only
    
- Unknown coupon → show “Invalid coupon”
    
- Discount more than total → cap at 0
    

### Tax

- Apply tax after discount
    
- For empty cart → tax must be 0
    

### UI/UX Edge Cases

- Updating qty too fast → UI must stay stable
    
- Very long product names → wrap correctly
    
- Cart empty state should be clean
    

---

# ❌ **📌 Failure Scenarios (Show depth of thinking)**

- User removes an item while typing in qty
    
- Subtotal or total becomes NaN due to invalid qty
    
- Coupon applied then cart emptied → coupon should reset
    
- Price updates not re-rendering UI due to stale DOM state
    
- Wrong coupon applied because of case-sensitivity
    
- User pastes text inside qty field → prevent non-numeric input
    
- Total price becomes negative
    
- Tax calculation breaks when discount = 100%
    

---

# 🎯 **📌 Acceptance Criteria (Pass/Fail Rules)**

### UI:

- Clean + readable
    
- No flicker on updates
    
- Cart updates instantly
    
- Discount + tax visible clearly
    

### Code:

- No duplicate code
    
- Functions:
    
    - addToCart()
        
    - removeFromCart()
        
    - updateQty()
        
    - applyDiscount()
        
    - calculateTotals()
        
    - renderCart()
        
- No inline events
    
- Proper variable names
    
- No global pollution
    
- No console errors
    

### Behavior:

- Qty updates must be smooth
    
- Total updates must ALWAYS be correct
    
- Coupon logic should be robust
    
- Cart empty state must show properly
    
- No hidden UI bugs
    

---

# 🧪 **📌 Test Cases**

|Action|Expected Output|
|---|---|
|Add “Laptop”|Cart shows Laptop qty 1|
|Add “Laptop” again|qty = 2|
|Click “+”|qty increments|
|Click “−”|qty decrements (min 1)|
|Remove item|Cart empty OR remaining items shown|
|Add 2 products|Total = sum of both|
|Apply “SAVE10”|price - 10%|
|Apply invalid coupon|show error|
|Apply coupon twice|apply only once|
|Tax = 18%|visible and correct|
|Empty cart then apply coupon|no discount applied|
|Change qty fast|totals always correct|
|Very long product name|wrapped without overflow|

---

# 🌟 **📌 Bonus Points (Optional but boosts score)**

- Animate cart updates
    
- Save entire cart in localStorage
    
- Undo remove item
    
- Quantity input directly editable with validation
    
- Show product image
    
- Add “Clear Cart” button
    

---

# Rahul — This is the EXACT industry-level shopping cart machine coding round.

If you want:

👉 **Start the live mock round**  
👉 **Get full working solution**  
👉 **Get a boilerplate HTML/CSS starter**  
👉 **Get backend version (Node.js API)**  
👉 **Get full-stack version (MERN)**

Just tell me — I’m with you.