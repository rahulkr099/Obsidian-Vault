This is a **very nice pattern used in production Node.js APIs**. It allows you to validate **`req.body`, `req.query`, and `req.params` using one middleware**. Interviewers like this because it shows **clean architecture and reusable design**.

I'll show you the pattern step-by-step.

---

# 1️⃣ Create a Generic Validation Middleware

Instead of writing many validators, create **one reusable validator**.

```js
// src/middlewares/validate.js
const Joi = require("joi");

function validate(schema) {
  return (req, res, next) => {

    const { value, error } = schema.validate(
      {
        body: req.body,
        query: req.query,
        params: req.params
      },
      {
        abortEarly: false,
        stripUnknown: true
      }
    );

    if (error) {
      return res.status(400).json({
        error: error.details.map(d => d.message)
      });
    }

    // sanitized values
    req.body = value.body;
    req.query = value.query;
    req.params = value.params;

    next();
  };
}

module.exports = validate;
```

---

# 2️⃣ Create Joi Schemas

Now your schemas can validate **body, query, and params together**.

Example for Todo.

```js
// src/validators/todo.validator.js
const Joi = require("joi");

exports.createTodoSchema = Joi.object({
  body: Joi.object({
    title: Joi.string().max(200).required(),
    description: Joi.string().allow("").optional(),
    status: Joi.string().valid("pending", "in-progress", "done"),
    priority: Joi.number().min(1).max(5),
    tags: Joi.array().items(Joi.string()),
    dueDate: Joi.date()
  })
});
```

---

# 3️⃣ Schema for Query Validation

For your **list API**.

```js
exports.listTodoSchema = Joi.object({
  query: Joi.object({
    page: Joi.number().min(1).default(1),
    limit: Joi.number().min(1).max(100).default(20),
    status: Joi.string().valid("pending", "in-progress", "done"),
    tag: Joi.string(),
    q: Joi.string(),
    sortBy: Joi.string()
  })
});
```

---

# 4️⃣ Schema for Params Validation

Example: validating `:id`.

```js
exports.todoIdSchema = Joi.object({
  params: Joi.object({
    id: Joi.string().length(24).required()
  })
});
```

(For MongoDB ObjectId)

---

# 5️⃣ Use in Routes

Your routes become **very clean**.

```js
const validate = require("../middlewares/validate");
const { createTodoSchema, listTodoSchema, todoIdSchema } = require("../validators/todo.validator");

router.post(
  "/todos",
  validate(createTodoSchema),
  todoController.create
);

router.get(
  "/todos",
  validate(listTodoSchema),
  todoController.list
);

router.patch(
  "/todos/:id",
  validate(todoIdSchema),
  todoController.update
);
```

---

# 6️⃣ What This Pattern Achieves

This architecture gives you:

✔ validation for **body**  
✔ validation for **query**  
✔ validation for **params**  
✔ automatic **field whitelisting** (`stripUnknown`)  
✔ reusable middleware  
✔ clean controllers

Controllers now assume **data is already valid**.

Example controller:

```js
exports.create = asyncHandler(async (req, res) => {

  const todo = await Todo.create(req.body);

  res.status(201).json({
    success: true,
    data: todo
  });

});
```

Very clean.

---

# 7️⃣ Why Interviewers Like This Pattern

Because it shows you understand:

- **middleware architecture**
    
- **separation of concerns**
    
- **input sanitization**
    
- **security practices**
    
- **reusable utilities**
    

This is **much stronger than validating directly inside controllers**.

---

# 8️⃣ Small Extra Tip (Very Impressive)

If you say this in an interview:

> "I validate body, query, and params using a reusable Joi middleware and sanitize inputs using stripUnknown before they reach controllers."

You will sound like a **backend engineer with production experience**.

---

If you'd like, I can also show you a **very clean folder structure for Node.js APIs that senior engineers use**, which will make your project look **very impressive in interviews**.