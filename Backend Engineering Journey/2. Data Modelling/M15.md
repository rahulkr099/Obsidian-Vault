# Module 15 — Audit Fields

> **Goal:** Learn how to track **who created, updated, deleted, or restored data**, making your backend more reliable, debuggable, and production-ready.

---

# Why This Module Matters

Imagine these situations:

A manager asks:

> "Who deleted this course?"

A customer asks:

> "When was my order updated?"

Your teammate asks:

> "Who changed the product price yesterday?"

Without audit fields:

```text
🤷 Nobody knows.
```

With audit fields:

```text
Created by: Rahul

Created at: 2026-08-01

Updated by: Amit

Updated at: 2026-08-03

Deleted by: Admin

Deleted at: 2026-08-05
```

You immediately have the answer.

Professional backend systems almost always include audit information.

---

# Where We Are

```text
Requirements
      ↓
Queries
      ↓
Entities
      ↓
Relationships
      ↓
Schema
      ↓
Validation
      ↓
Constraints
      ↓
Indexes
      ↓
Growth Planning
      ↓
Soft Delete
      ↓
Audit Fields   ← You are here
      ↓
Security Review
```

---

# What Are Audit Fields?

Audit fields store information about **changes** made to a record.

Typical questions they answer:

- Who created this?
    
- When was it created?
    
- Who updated it?
    
- When was it updated?
    
- Who deleted it?
    
- When was it deleted?
    
- Who restored it?
    

Audit fields improve:

- Accountability
    
- Debugging
    
- Security
    
- Compliance
    

---

# The Most Common Audit Fields

Nearly every production application includes:

```javascript
{
    createdAt,
    updatedAt
}
```

These are the minimum.

Many applications also include:

```javascript
{
    createdBy,
    updatedBy,
    deletedAt,
    deletedBy
}
```

---

# 1. createdAt

Stores when the record was created.

Example:

```javascript
{
    createdAt: "2026-08-03T10:15:20Z"
}
```

Uses:

- Sort newest records
    
- Analytics
    
- Reports
    
- Activity history
    

---

# 2. updatedAt

Stores the latest modification time.

Example:

```javascript
{
    updatedAt: "2026-08-05T08:10:42Z"
}
```

Useful for:

- "Last edited"
    
- Cache invalidation
    
- Synchronization
    
- Debugging
    

---

# 3. createdBy

Stores who created the record.

Example:

```javascript
{
    createdBy: ObjectId("user123")
}
```

Example:

Course:

```text
Created by Rahul
```

Later:

```text
Rahul leaves the company.
```

Still know who originally created it.

---

# 4. updatedBy

Tracks who last modified the record.

Example:

```javascript
{
    updatedBy: ObjectId("admin456")
}
```

Suppose:

Product price changed.

Now you know:

```text
Updated by Admin
```

---

# 5. deletedAt

Already discussed in Module 14.

Example:

```javascript
{
    deletedAt: Date
}
```

---

# 6. deletedBy

Stores who deleted it.

Example:

```javascript
{
    deletedBy: ObjectId("admin123")
}
```

Very useful in admin systems.

---

# 7. restoredAt

Some applications also store:

```javascript
{
    restoredAt,
    restoredBy
}
```

Useful when recovery matters.

Example:

Hospital

Legal

Banking

Government

---

# Automatic vs Manual Audit Fields

## Automatic

Mongoose can automatically manage:

```javascript
timestamps: true
```

This creates:

```javascript
createdAt

updatedAt
```

Automatically.

---

## Manual

Fields like:

```javascript
createdBy

updatedBy

deletedBy
```

Must be set by your application.

Usually in the service layer.

---

# Example — Blog Application

Post:

```javascript
{
    _id,

    title,

    content,

    createdAt,

    updatedAt,

    createdBy,

    updatedBy
}
```

Now you know:

- When the blog was written.
    
- Who wrote it.
    
- Who edited it.
    

---

# Example — Todo App

Task:

```javascript
{
    title,

    completed,

    createdAt,

    updatedAt
}
```

Enough for a personal application.

No need for:

```text
createdBy
```

because every task belongs to one user.

Keep it simple.

---

# Example — Learning Management System

Course:

```javascript
{
    title,

    teacherId,

    createdAt,

    updatedAt,

    createdBy,

    updatedBy,

    deletedAt,

    deletedBy
}
```

Excellent for universities.

---

# Example — E-commerce

Product:

```javascript
{
    name,

    price,

    stock,

    createdAt,

    updatedAt,

    updatedBy
}
```

Now managers know who changed prices.

---

# Example — Banking

Transaction:

```javascript
{
    amount,

    fromAccount,

    toAccount,

    createdAt
}
```

Notice:

Transactions usually should **never** be updated.

Only created.

This is an example of an immutable entity.

---

# Immutable vs Mutable Records

## Mutable

Can change.

Examples:

```text
User Profile

Blog

Product

Course
```

Need:

```text
updatedAt
```

---

## Immutable

Never changes after creation.

Examples:

```text
Transaction

Invoice

Payment Receipt

Audit Log
```

May only need:

```text
createdAt
```

---

# Audit Fields and APIs

Example:

```http
POST /posts
```

Service:

```text
createdBy = req.user.id
```

---

Example:

```http
PUT /posts/:id
```

Service:

```text
updatedBy = req.user.id
```

---

Example:

```http
DELETE /posts/:id
```

Instead of deleting:

```text
deletedAt = now()

deletedBy = req.user.id
```

---

# Audit Fields and Security

Suppose:

Admin changes salary.

Later:

Employee complains.

Audit fields reveal:

```text
Updated by:

Admin A

Time:

09:45 AM
```

Very important.

---

# Audit Fields vs Activity Logs

Don't confuse them.

Audit Fields:

Stored **inside the record**.

Example:

```javascript
{
    updatedBy,

    updatedAt
}
```

---

Activity Log:

Separate collection.

Example:

```javascript
{
    user,

    action,

    timestamp,

    ip,

    browser
}
```

Audit fields answer:

```text
Who last updated this record?
```

Activity logs answer:

```text
What actions has this user performed over time?
```

---

# Real Example

User edits profile five times.

Audit Fields:

```text
updatedAt

↓

Latest update only.
```

Activity Log:

```text
Update 1

Update 2

Update 3

Update 4

Update 5
```

Complete history.

---

# When NOT to Add Every Audit Field

Small Notes App:

```javascript
{
    createdAt,

    updatedAt
}
```

Enough.

---

Enterprise HR Software:

```javascript
{
    createdAt,

    updatedAt,

    createdBy,

    updatedBy,

    deletedAt,

    deletedBy,

    restoredAt,

    restoredBy
}
```

Needed.

Choose based on business requirements.

---

# Common Beginner Mistakes

## Mistake 1

Not storing timestamps.

Later impossible to answer:

```text
When was this created?
```

---

## Mistake 2

Trusting frontend timestamps.

Wrong:

```javascript
createdAt

↓

Client
```

Backend should generate timestamps.

---

## Mistake 3

Updating `createdAt`.

Never.

`createdAt` should never change.

---

## Mistake 4

Forgetting `updatedBy`.

Especially in admin applications.

---

## Mistake 5

Using local server time incorrectly.

Prefer storing timestamps in UTC.

Convert to local time only when displaying them to users.

---

# Best Practices

- Enable automatic timestamps where possible.
    
- Store `createdBy` and `updatedBy` for shared resources.
    
- Use `deletedAt` and `deletedBy` with soft delete.
    
- Keep immutable records truly immutable.
    
- Generate timestamps on the backend, not on the client.
    
- Store times in UTC.
    
- Add only the audit fields your application genuinely needs.
    

---

# Audit Field Decision Matrix

|Entity|createdAt|updatedAt|createdBy|updatedBy|deletedAt|deletedBy|
|---|---|---|---|---|---|---|
|User|✅|✅|❌|❌|✅|❌|
|Blog Post|✅|✅|✅|✅|✅|✅|
|Product|✅|✅|✅|✅|✅|✅|
|Comment|✅|✅|✅|✅|✅|✅|
|Order|✅|Limited|✅|Limited|Usually ❌|❌|
|Transaction|✅|❌|System|❌|❌|❌|

Notice that not every entity needs every audit field.

---

# Mongoose Example

```javascript
const postSchema = new mongoose.Schema(
  {
    title: String,
    content: String,

    createdBy: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
    },

    updatedBy: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
    },

    deletedAt: Date,

    deletedBy: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
    },
  },
  {
    timestamps: true, // createdAt and updatedAt
  }
);
```

Notice how `timestamps: true` saves you from manually managing two common audit fields.

---

# Module 15 Summary

By the end of this module, you should be able to:

- Explain the purpose of audit fields.
    
- Choose the appropriate audit fields for different entities.
    
- Distinguish between audit fields and activity logs.
    
- Know when records should be mutable or immutable.
    
- Use automatic timestamps and manual user-tracking fields effectively.
    
- Design schemas that support accountability, debugging, and compliance.
    

---

# Mini Exercise

Design the audit fields for an **Inventory Management System**.

Entities:

```text
Warehouse

Product

Inventory

PurchaseOrder

Supplier

StockMovement
```

For each entity, decide:

1. Which audit fields are required?
    
2. Which entities are mutable and which are immutable?
    
3. Should `createdBy` and `updatedBy` be stored?
    
4. Should `deletedAt` and `deletedBy` be supported?
    
5. Would an activity log be useful in addition to audit fields?
    

> **Next Module:** **Module 16 — Security Review**, where you'll learn how to review your data model from a security perspective by identifying sensitive fields, protecting secrets, preventing data leaks, and designing schemas that follow the principle of least privilege.