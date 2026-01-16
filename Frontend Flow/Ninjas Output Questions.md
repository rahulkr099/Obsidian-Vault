```javascript
Q. Predict the output of following JavaScript code

  state={
     value:1
  }
  componentDidMount() {
     console.log("Mounted")
     this.setState({value:2})  
  }
  render() {
     console.log("Rendered")
     return (
        <div>
          Hi
        <div/>
     )
  }
```

Great question 👍 This is a **very common interview favorite**, and you’re thinking in the right direction by asking _predict the output_.

Let’s go step by step in **simple words**.

---

## ✅ The code (React class component logic)

```js
state = {
  value: 1
}

componentDidMount() {
  console.log("Mounted")
  this.setState({ value: 2 })
}

render() {
  console.log("Rendered")
  return (
    <div>
      Hi
    </div>
  )
}
```

---

## 🧠 How React runs this code

### 1️⃣ **Initial render (first time)**

When the component loads:

- `render()` runs first
    
- Console prints:
    

```
Rendered
```

---

### 2️⃣ **Component is mounted**

After the first render is finished:

- `componentDidMount()` runs
    
- Console prints:
    

```
Mounted
```

- Inside `componentDidMount`, you call `setState({ value: 2 })`
    

---

### 3️⃣ **State update → re-render**

Calling `setState` **always triggers render again**:

- `render()` runs again
    
- Console prints:
    

```
Rendered
```

---

## ✅ Final Output (Order Matters)

```
Rendered
Mounted
Rendered
```

✔️ **This is the correct answer**

---

## 🔑 Key Interview Takeaways (Very Important)

- `render()` runs **before** `componentDidMount`
    
- `componentDidMount()` runs **only once**
    
- `setState()` inside `componentDidMount` causes **one extra render**
    
- `render()` can run **multiple times**
    

---

## 🚀 Smart Interview Tip (Bonus)

If the interviewer asks:

👉 _“Why does render run twice?”_

You say:

> Because `setState` inside `componentDidMount` updates the state, which triggers a re-render.

💯 That answer shows **real React understanding**, not rote learning.

---

## 💡 How to Level This Up (Innovative Practice Idea)

Try this next:

- Add `console.log(this.state.value)` inside `render`
    
- Predict values before running
    
- Do the same experiment with:
    
    - `constructor`
        
    - `componentDidUpdate`
        
    - `useEffect` (functional components)
        

This builds **intuition**, not fear.

---

If you want, I can now:

- Convert this to **functional component**
    
- Ask you a **mock interview follow-up**
    
- Give **5 similar predict-the-output questions**
    

Just tell me 👍

```javascript
 Problem statement

What will the following JavaScript code print in the console?

let People = function(person, age) { 
        this.person = person; 
        this.age = age; 
        this.info = function() { 
            console.log(this);  
           setTimeout(() => {  
            console.log(this.person + " is " + this.age + " years old"); 
           }, 3000); 
        } 
    }  
let person1 = new People('John', 21); 
person1.info();

```

Nice one 👍  
This question checks your **understanding of `this`, closures, and arrow functions** — very popular in interviews.

Let’s break it calmly and clearly.

---

## ✅ The Code

```js
let People = function(person, age) { 
    this.person = person; 
    this.age = age; 
    this.info = function() { 
        console.log(this);  

        setTimeout(() => {  
            console.log(this.person + " is " + this.age + " years old"); 
        }, 3000); 
    } 
}  

let person1 = new People('John', 21); 
person1.info();
```

---

## 🧠 Step-by-Step Execution

### 1️⃣ Object creation

```js
let person1 = new People('John', 21);
```

This creates an object like:

```js
{
  person: "John",
  age: 21,
  info: function() { ... }
}
```

---

### 2️⃣ Calling `info()`

```js
person1.info();
```

Inside `info()`:

#### 🔹 First console.log

```js
console.log(this);
```

👉 Here, `this` refers to **`person1` object**

So it prints:

```
People { person: "John", age: 21, info: ƒ }
```

_(Exact format may vary slightly by browser)_

---

### 3️⃣ `setTimeout` with arrow function

```js
setTimeout(() => {
  console.log(this.person + " is " + this.age + " years old");
}, 3000);
```

🔑 **Important concept**  
Arrow functions **do NOT have their own `this`**.  
They **inherit `this` from their surrounding scope**.

So here:

- `this` inside arrow function = `this` of `info()`
    
- And `this` of `info()` = `person1`
    

✅ No `this` confusion happens 🎯

---

## ⏱️ After 3 seconds…

This line runs:

```
John is 21 years old
```

---

## ✅ Final Console Output (in order)

Immediately:

```
People { person: "John", age: 21, info: ƒ }
```

After 3 seconds:

```
John is 21 years old
```

---

## 🔥 Why This Question Is Important (Interview Insight)

If the arrow function was replaced with a **normal function**:

```js
setTimeout(function() {
  console.log(this.person);
}, 3000);
```

❌ `this` would be `window` (or `undefined` in strict mode)

That’s why arrow functions are commonly used in:

- `setTimeout`
    
- `setInterval`
    
- event handlers
    
- React callbacks
    

---

## 💡 Improvement Idea (Try This Yourself)

To master `this`, do this mini-practice:

- Replace arrow function with normal function
    
- Try `.bind(this)`
    
- Try storing `const self = this`
    
- Try same logic inside **React** or **class syntax**
    

This will make your JS fundamentals **rock solid** 🚀

---

If you want, I can now:

- Convert this to **ES6 class**
    
- Give you **5 tricky `this` output questions**
    
- Show how this behaves in **React / Node / browser**
    

Just say the word 😊

```javascript
What will be the output of the JavaScript code below?

function Abc() {
"use strict"
this.a = 25;
return {a: 35, b: 44};
}
var obj = new Abc();
console.log(obj.a, obj.b);

```

Great question 👍  
This one is **small but very powerful**. It tests how `new`, `this`, `return`, and `"use strict"` work together.

Let’s walk through it slowly and clearly.

---

## ✅ The Code

```js
function Abc() {
  "use strict"
  this.a = 25;
  return { a: 35, b: 44 };
}

var obj = new Abc();
console.log(obj.a, obj.b);
```

---

## 🧠 Step-by-Step Thinking

### 1️⃣ What does `new Abc()` do?

When you use `new`:

- A **new empty object** is created
    
- `this` points to that object
    
- The function runs
    
- By default, `this` is returned
    

---

### 2️⃣ Inside the function

```js
this.a = 25;
```

At this point, the object looks like:

```js
{ a: 25 }
```

---

### 3️⃣ Important line (the trick 🔥)

```js
return { a: 35, b: 44 };
```

🔑 **Rule to remember forever**:

> If a constructor returns an **object**, that object **replaces `this`**

So:

- The `{ a: 35, b: 44 }` object is returned
    
- The original `this.a = 25` is **ignored**
    

---

### 4️⃣ Value of `obj`

```js
obj = { a: 35, b: 44 }
```

---

## ✅ Final Output

```txt
35 44
```

---

## ⚠️ Does `"use strict"` matter here?

👉 **No impact in this case**

Why?

- You are using `new`
    
- `this` is correctly bound
    
- Strict mode mainly affects cases where `this` becomes `undefined`
    

---

## 🧩 Interview Gold Summary

- `new` creates a new object
    
- `this` refers to that object
    
- Returning an **object** overrides `this`
    
- Returning a **primitive** does NOT override `this`
    

---

## 💡 Try This to Level Up

Change this line:

```js
return 10;
```

Now predict the output 😉

👉 You’ll see:

```txt
25 undefined
```

Why? Because primitives don’t replace `this`.

---

If you want, I can:

- Give **5 constructor trick questions**
    
- Compare this with **class syntax**
    
- Explain how this behaves in **React / Node**
    

Just tell me 🚀