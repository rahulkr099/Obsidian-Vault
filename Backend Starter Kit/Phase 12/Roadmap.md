# Phase 12 — Services & Business Logic

Yes, Rahul. **Phase 12 is the next phase**, and this is one of the most important phases in your backend journey.

According to the roadmap we created, Phase 12 is:

> **Services & Business Logic**

Your starter pack specifically has a `services/` layer, including `auth.service.js` and `password.service.js`, and the purpose of this phase is to understand why that layer exists rather than simply copying it.

You have already completed **Phase 11 — Controllers**, so now we make the next step:

```text
Route
  ↓
Middleware
  ↓
Controller       ← Phase 11
  ↓
Service          ← Phase 12
  ↓
Repository       ← Phase 13
  ↓
Model
  ↓
MongoDB
```

---

# 🎯 Phase 12 Goal

By the end of Phase 12, you should be able to look at this:

```js
const login = async (req, res) => {
    const user = await User.findOne({ email: req.body.email });

    if (!user) {
        return res.status(404).json({
            message: "User not found"
        });
    }

    const isValid = await bcrypt.compare(
        req.body.password,
        user.password
    );

    if (!isValid) {
        return res.status(401).json({
            message: "Invalid password"
        });
    }

    // generate token
    // save refresh token
    // send email
    // etc...
};
```

and immediately think:

> **"This controller is doing too much. The business logic belongs in a service."**

That is the main skill we are going to develop.

---

# 📚 Phase 12 Lessons

We'll use **20 lessons**, just like the roadmap specifies.

```text
12.1  What is Business Logic?
12.2  Why Controllers Shouldn't Contain Business Logic
12.3  What is a Service?
12.4  Controller vs Service
12.5  Identifying Business Rules
12.6  Moving Logic into a Service
12.7  Service Inputs and Outputs
12.8  Service Error Handling
12.9  Service Dependencies
12.10 Calling Repositories from Services

12.11 Authentication Service
12.12 User Service
12.13 CRUD Service
12.14 Transactions and Business Operations
12.15 Service Composition
12.16 Avoiding Giant Services
12.17 Service Naming Conventions
12.18 Common Service Mistakes
12.19 Testing Services
12.20 Build a Complete Service Layer
```

---

# 🧠 The Core Idea

Imagine a restaurant.

```text
Customer
   ↓
Waiter
   ↓
Kitchen
   ↓
Ingredients
```

The waiter doesn't cook the food.

The waiter takes the order:

```text
"I want Pizza."
```

The kitchen decides:

```text
How should the pizza be prepared?
What ingredients are needed?
How should it be cooked?
```

Backend:

```text
Frontend
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

So:

### Controller = Waiter

Handles HTTP.

### Service = Kitchen

Handles business decisions.

### Repository = Database worker

Handles data access.

This separation is the foundation of this phase.

---

# 🗺️ Complete Phase 12 Architecture

By the end:

```text
                     HTTP Request
                          │
                          ▼
                       ROUTE
                          │
                          ▼
                     MIDDLEWARE
                          │
                          ▼
                     CONTROLLER
                          │
                          │
                          ▼
                    ┌───────────┐
                    │  SERVICE  │
                    │           │
                    │ Business  │
                    │  Logic    │
                    └─────┬─────┘
                          │
                          ▼
                     REPOSITORY
                          │
                          ▼
                        MODEL
                          │
                          ▼
                       MongoDB
```

The important boundary is:

```text
HTTP world
──────────────
Route
Middleware
Controller

Application world
──────────────────
Service

Data world
────────────
Repository
Model
MongoDB
```

This separation makes large applications easier to maintain.

---

# 🔥 What We'll Build During Phase 12

We'll use a small example application throughout the phase:

```text
User
```

Then we'll gradually build:

```text
user.service.js
```

and eventually:

```text
services/
├── auth.service.js
├── user.service.js
├── password.service.js
└── todo.service.js
```

This closely matches the architecture you're ultimately trying to understand.

---

# 🚦 One Important Rule

During Phase 12, **don't worry about repositories too much yet**.

We'll initially use:

```text
Controller
   ↓
Service
   ↓
Model
```

Then Phase 13 will introduce:

```text
Controller
   ↓
Service
   ↓
Repository
   ↓
Model
```

This gradual approach is intentional.

Otherwise you'll have too many new concepts at once.

---

# Phase 12 Learning Strategy

Each lesson will follow this structure:

### 1. Simple explanation

No complicated terminology first.

### 2. Why it exists

This is the most important part.

### 3. Real-world analogy

So you can build intuition.

### 4. Request-flow diagram

For example:

```text
POST /users
     ↓
Controller
     ↓
User Service
     ↓
User Model
     ↓
MongoDB
```

### 5. Small code example

We'll avoid giant files.

### 6. Line-by-line explanation

You'll understand **why** every important line exists.

### 7. Common mistakes

For example:

```text
❌ Fat controllers
❌ Services returning HTTP responses
❌ Services accessing req/res
❌ Giant services
❌ Mixing database queries everywhere
```

### 8. Mini exercise

You'll implement a small part yourself.

### 9. Interview questions

We'll reinforce the concept.

### 10. Starter-pack connection

Finally:

> "Now look at how this idea appears in your actual starter."

That last step is important because your goal is ultimately to build the starter from scratch.

---

# 🏗️ Final Transformation

At the beginning of Phase 12:

```js
const createUser = async (req, res) => {

    // validate

    // check user

    // hash password

    // create user

    // send email

    // generate token

    // response
};
```

Everything is inside the controller.

By the end:

```js
const createUser = asyncHandler(async (req, res) => {

    const user = await userService.createUser(req.body);

    res.status(201).json({
        success: true,
        data: user
    });
});
```

And:

```js
const createUser = async (userData) => {

    // business logic

};
```

Eventually, after Phase 13:

```text
Controller
     ↓
userService.createUser()
     ↓
userRepository
     ↓
User Model
     ↓
MongoDB
```

That's the architectural transformation we're after.

---

# 📌 Phase 12 Progress

We'll go one lesson at a time:

```text
12.1  ← Start here
12.2
12.3
12.4
12.5
12.6
12.7
12.8
12.9
12.10
12.11
12.12
12.13
12.14
12.15
12.16
12.17
12.18
12.19
12.20
```

**Next lesson: `12.1 — What is Business Logic?`**

And I recommend we make this one very practical: we'll take a **bad/fat controller**, identify exactly which lines are business logic, and then move them into a service step by step.