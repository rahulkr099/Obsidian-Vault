Alright Rahul, let’s build a **perfect machine-coding-round Shopping Cart project** using only **HTML, CSS, and JavaScript** — clean, testable, and similar to what big companies use in rounds.

I’ll give you:

✅ Problem statement (interview-style)  
✅ Full working code  
✅ Add to cart  
✅ Remove from cart  
✅ Update quantity  
✅ Cart total recalculation  
✅ Clean UI  
✅ Bonus “improvement tasks” to practice deeper patterns

Let’s go!

---

# 🚀 **Machine Coding Round Project: Shopping Cart**

This is one of the MOST asked coding-round problems.

Your main tasks:

- Show a list of products
    
- Allow user to **add to cart**
    
- Show cart items
    
- **Increase / Decrease** quantity
    
- Remove item
    
- Automatically **update total**
    

No frameworks, only pure JS.

---

# 📁 **Folder Structure**

```
shopping-cart/
│── index.html
│── style.css
└── script.js
```

---

# 🧱 **1. index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Shopping Cart (Machine Coding Round)</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>

    <h1>Shopping Cart</h1>

    <div class="container">

        <div class="products">
            <h2>Products</h2>
            <div id="product-list"></div>
        </div>

        <div class="cart">
            <h2>Your Cart</h2>
            <div id="cart-items"></div>

            <div class="cart-total">
                Total: ₹<span id="total">0</span>
            </div>
        </div>

    </div>

    <script src="script.js"></script>
</body>
</html>
```

---

# 🧱 **2. style.css**

```css
body {
    font-family: Arial, sans-serif;
    background: #f7f7f7;
    padding: 30px;
}

h1 {
    text-align: center;
    margin-bottom: 25px;
}

.container {
    display: flex;
    gap: 30px;
    justify-content: center;
}

.products, .cart {
    width: 350px;
    background: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

.product, .cart-item {
    border-bottom: 1px solid #eee;
    padding: 12px 0;
}

button {
    padding: 8px 14px;
    border: none;
    background: black;
    color: white;
    border-radius: 5px;
    cursor: pointer;
}

button:disabled {
    background: gray;
}

.cart-item-controls {
    margin-top: 8px;
    display: flex;
    gap: 8px;
    align-items: center;
}

.qty-btn {
    background: #ddd;
    color: black;
    width: 28px;
    height: 28px;
    border-radius: 4px;
}

.remove-btn {
    background: red;
    color: white;
}

.cart-total {
    font-size: 20px;
    font-weight: bold;
    margin-top: 15px;
}
```

---

# 🧱 **3. script.js**

```javascript
// Dummy product data
const products = [
    { id: 1, name: "Laptop", price: 45000 },
    { id: 2, name: "Headphones", price: 1500 },
    { id: 3, name: "Keyboard", price: 700 },
    { id: 4, name: "Smartphone", price: 20000 },
];

const productList = document.getElementById("product-list");
const cartItems = document.getElementById("cart-items");
const totalSpan = document.getElementById("total");

let cart = {};

// Render products
function renderProducts() {
    productList.innerHTML = "";

    products.forEach(p => {
        const div = document.createElement("div");
        div.classList.add("product");

        div.innerHTML = `
            <strong>${p.name}</strong> - ₹${p.price}
            <br>
            <button onclick="addToCart(${p.id})">Add to Cart</button>
        `;

        productList.appendChild(div);
    });
}

// Add item to cart
function addToCart(id) {
    if (!cart[id]) {
        const product = products.find(p => p.id === id);
        cart[id] = { ...product, qty: 1 };
    } else {
        cart[id].qty++;
    }
    renderCart();
}

// Remove item
function removeItem(id) {
    delete cart[id];
    renderCart();
}

// Update quantity
function changeQty(id, amount) {
    cart[id].qty += amount;

    if (cart[id].qty <= 0) 
        removeItem(id);
    }

    renderCart();
}

// Render cart
function renderCart() {
    cartItems.innerHTML = "";
    let total = 0;

    Object.values(cart).forEach(item => {
        const div = document.createElement("div");
        div.classList.add("cart-item");

        const itemTotal = item.qty * item.price;
        total += itemTotal;

        div.innerHTML = `
            <strong>${item.name}</strong> - ₹${itemTotal}
            <div class="cart-item-controls">
                <button class="qty-btn" onclick="changeQty(${item.id}, -1)">-</button>
                ${item.qty}
                <button class="qty-btn" onclick="changeQty(${item.id}, 1)">+</button>
                <button class="remove-btn" onclick="removeItem(${item.id})">Remove</button>
            </div>
        `;

        cartItems.appendChild(div);
    });

    totalSpan.textContent = total;
}

// Initialize
renderProducts();
renderCart();
```

---

# 🎯 **Interview Concepts You Practiced**

You covered:

- State management (cart object)
    
- DOM updates
    
- Event handling
    
- Computation of totals
    
- Reusability (render functions)
    
- Data flow
    
- Safe quantity updates
    
- Clean structure
    

This is exactly the structure interviewers expect.

---

# 🔥 **Level-Up Tasks (Highly Recommended)**

To make your solution _stand out_, practice these:

### ⭐ 1. Add "Clear Cart" button

Resets everything.

### ⭐ 2. Add localStorage persistence

Cart stays after page refresh.

### ⭐ 3. Add product images and styling

Make it look more real.

### ⭐ 4. Add checkout modal

Show summary + confirm.

### ⭐ 5. Add promo code

Apply discount if code is "RAHUL10".

### ⭐ 6. Add "undo remove" with toast notification.

### ⭐ 7. Add dynamic product search + filter.

### ⭐ 8. Add stock limit (cannot increase qty beyond stock).

---

# 🌟 Want more practice?

I can give you:

- **Wishlist + Cart combined project**
    
- **E-commerce product grid with filters**
    
- **Mini flipkart clone**
    
- **Machine coding round PDF problem statements**
    
- **Class-based or OOP version**
    

Just tell me and I’ll prepare it!