You already wrote **very good controllers**, but right now they still contain **validation logic inside them** (like allowedFields, ObjectId checks, pagination checks, etc.).  
Using **Joi middleware**, we will move **all validation out of controllers** so controllers become **very small and clean**. This is the pattern many production APIs use.

I'll show you the **step-by-step refactor**.

---

# Step 1 — Create Validation Middleware

Create a reusable middleware.

`src/middlewares/validate.js`

```js
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

    req.body = value.body;
    req.query = value.query;
    req.params = value.params;

    next();
  };
}

module.exports = validate;
```

What this does:

✔ validates body  
✔ validates query  
✔ validates params  
✔ removes unknown fields automatically

---

# Step 2 — Create Joi Schemas

Create a folder:

```
src/validators
```

Create:

`todo.validator.js`

```js
const Joi = require("joi");

exports.createTodoSchema = Joi.object({
  body: Joi.object({
    title: Joi.string().max(200).required(),
    description: Joi.string().allow("").optional(),
    status: Joi.string().valid("pending","in-progress","done"),
    priority: Joi.number().min(1).max(5),
    tags: Joi.array().items(Joi.string()),
    dueDate: Joi.date()
  })
});
```

---

## Update Todo Schema

```js
exports.updateTodoSchema = Joi.object({
  params: Joi.object({
    id: Joi.string().length(24).required()
  }),
  body: Joi.object({
    title: Joi.string().max(200),
    description: Joi.string().allow(""),
    status: Joi.string().valid("pending","in-progress","done"),
    priority: Joi.number().min(1).max(5),
    tags: Joi.array().items(Joi.string()),
    dueDate: Joi.date()
  }).min(1)
});
```

---

## List Query Schema

```js
exports.listTodoSchema = Joi.object({
  query: Joi.object({
    page: Joi.number().min(1).default(1),
    limit: Joi.number().min(1).max(100).default(20),
    status: Joi.string().valid("pending","in-progress","done"),
    tag: Joi.string(),
    q: Joi.string(),
    sortBy: Joi.string()
  })
});
```

---

## ID Param Schema

```js
exports.todoIdSchema = Joi.object({
  params: Joi.object({
    id: Joi.string().length(24).required()
  })
});
```

---

# Step 3 — Clean Your Controllers

After validation middleware, controllers become **much simpler**.

Example **create controller**:

```js
export const create = asyncHandler(async (req, res) => {

  const todo = await Todo.create(req.body);

  await Activity.create({
    todoId: todo._id,
    action: "create",
    userId: req.user._id,
    payload: req.body
  });

  res.status(201).json({
    success: true,
    data: todo
  });

});
```

Notice:

❌ no manual field whitelist  
❌ no payload validation  
❌ no type checking

Joi already did it.

---

## Update Controller (Clean Version)

```js
export const update = asyncHandler(async (req, res) => {

  const todo = await Todo.findOneAndUpdate(
    { _id: req.params.id, softDelete: false },
    {
      $set: req.body,
      $inc: { version: 1 }
    },
    { new: true, runValidators: true }
  );

  if (!todo) throw new AppError("Todo not found", 404);

  await Activity.create({
    todoId: todo._id,
    action: "update",
    userId: req.user._id,
    payload: req.body
  });

  res.json({
    success: true,
    data: todo
  });

});
```

Much cleaner.

---

# Step 4 — Apply Middleware in Routes

Example routes:

```js
const validate = require("../middlewares/validate");
const {
  createTodoSchema,
  updateTodoSchema,
  listTodoSchema,
  todoIdSchema
} = require("../validators/todo.validator");

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
  validate(updateTodoSchema),
  todoController.update
);

router.get(
  "/todos/:id",
  validate(todoIdSchema),
  todoController.get
);
```

---

# Step 5 — Final Architecture

Your project will look like this:

```
src
 ├── controllers
 │     todo.controller.js
 │
 ├── validators
 │     todo.validator.js
 │
 ├── middlewares
 │     validate.js
 │
 ├── routes
 │     todo.routes.js
 │
 ├── utils
 │     asyncHandler.js
 │     AppError.js
 │     parseSort.js
 │
 └── models
       todo.model.js
```

This structure is **very impressive for interviews**.

---

# Why This Pattern Is Strong

It shows:

✔ middleware architecture  
✔ separation of concerns  
✔ reusable validation  
✔ sanitized inputs  
✔ clean controllers

Your controller size will shrink **by about 40-50%**.

---

✅ If you want, I can also show you **one more improvement senior backend engineers use with Joi**:  
**centralized error formatter** so validation errors look clean and consistent across the whole API.