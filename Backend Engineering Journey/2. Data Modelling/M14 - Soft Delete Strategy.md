# Module 14 — Soft Delete Strategy

> **Goal:** Learn how professional backend systems handle deletion safely by using **soft deletes**, allowing data recovery, auditing, and compliance instead of permanently removing records immediately.

---

# Why This Module Matters

One of the biggest mistakes beginners make is:

```javascript
await User.findByIdAndDelete(id);
```

or

```javascript
await Post.deleteOne({ _id: id });
```

It works...

Until someone asks:

> "Can you restore my deleted account?"

or

> "Who deleted this post yesterday?"

or

> "Can we recover that order?"

If the data is permanently deleted,

the answer is:

> **No.**

Professional applications rarely delete important data immediately.

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
Soft Delete Strategy   ← You are here
      ↓
Audit Fields
      ↓
Security Review
```

---

# What Is a Soft Delete?

Instead of removing a record,

mark it as deleted.

Example:

Instead of:

```text
DELETE Post
```

Do:

```javascript
{
    status: "deleted"
}
```

or

```javascript
{
    deletedAt: "2026-08-03T15:20:00Z"
}
```

The record still exists.

The application simply hides it.

---

# Hard Delete vs Soft Delete

## Hard Delete

```text
Database

↓

Record Removed Forever
```

Example:

```javascript
await User.deleteOne({ _id });
```

Result:

```text
❌ Cannot recover.
```

---

## Soft Delete

```text
Database

↓

Record Still Exists

↓

Hidden From Users
```

Example:

```javascript
{
    deletedAt: Date.now()
}
```

Result:

```text
✅ Can restore later.
```

---

# Why Companies Use Soft Delete

Imagine these applications.

## Gmail

Delete email.

Can restore from Trash.

---

## YouTube

Delete video.

Creators often have time to recover it.

---

## Instagram

Deleted posts can be restored.

---

## E-commerce

Deleted orders remain for:

- Accounting
    
- Auditing
    
- Legal reasons
    

---

Professional applications almost always need deleted data.

---

# Common Soft Delete Fields

There are three common approaches.

---

## Option 1 — Boolean

```javascript
{
    isDeleted: true
}
```

Simple.

But doesn't tell you:

- When?
    
- By whom?
    

---

## Option 2 — Status

```javascript
{
    status: "deleted"
}
```

Good when the entity already has states.

Example:

```text
draft

published

archived

deleted
```

---

## Option 3 — deletedAt

Most common.

```javascript
{
    deletedAt: Date
}
```

Example:

```javascript
{
    deletedAt: "2026-08-03T10:20:00Z"
}
```

If:

```text
deletedAt = null
```

The record is active.

If:

```text
deletedAt != null
```

The record is deleted.

---

# Even Better

Many production systems store:

```javascript
{
    deletedAt,
    deletedBy
}
```

Example:

```javascript
{
    deletedAt: "...",
    deletedBy: adminId
}
```

Now you know:

- Who deleted it.
    
- When it happened.
    

---

# Example 1 — Blog Application

Instead of:

```javascript
delete post
```

Do:

```javascript
{
    status: "deleted"
}
```

Homepage query:

```javascript
find({

status:"published"

})
```

Deleted posts automatically disappear.

---

# Example 2 — Todo App

Instead of:

```javascript
delete task
```

Update:

```javascript
{
    deletedAt: Date.now()
}
```

Restore:

```javascript
{
    deletedAt: null
}
```

Simple.

---

# Example 3 — E-commerce

Never hard delete:

```text
Orders
```

Why?

Accounting.

Invoices.

Taxes.

Refunds.

Orders usually stay forever.

Sometimes only:

```text
status

↓

cancelled
```

---

# Example 4 — User Account

Instead of deleting:

```text
User
```

Mark:

```javascript
{
    status: "inactive"
}
```

or

```javascript
{
    deletedAt
}
```

This preserves:

- Orders
    
- Posts
    
- Comments
    
- Analytics
    

---

# Example 5 — URL Shortener

Delete URL.

Instead:

```javascript
{
    status: "disabled"
}
```

Redirect:

```text
404
```

or

```text
410 Gone
```

The analytics still remain.

---

# Step 1 — Decide Which Entities Need Soft Delete

Not every entity should use it.

Example:

## User

Yes.

---

## Post

Yes.

---

## Order

Yes.

---

## Product

Usually yes.

---

## OTP

No.

Delete permanently.

---

## Session Token

No.

Expire automatically.

---

## Cache

No.

Delete freely.

---

# Step 2 — Update Queries

Suppose:

Before:

```javascript
find()
```

Now:

```javascript
find({

deletedAt:null

})
```

or

```javascript
find({

status:{

$ne:"deleted"

}

})
```

Every query must ignore deleted data unless explicitly requested.

---

# Step 3 — Restore Support

Suppose:

User deletes a blog.

Later:

```text
Restore
```

Simply:

```javascript
deletedAt = null
```

No complex recovery process.

---

# Step 4 — Cleanup Strategy

Soft delete does not mean:

Keep forever.

Many companies run cleanup jobs.

Example:

```text
Deleted

↓

30 Days

↓

Permanent Delete
```

Cron Job:

```text
Every Night

↓

Delete Expired Records
```

This keeps the database clean.

---

# Example Cleanup Policies

## Notes App

```text
Trash

↓

30 days

↓

Permanent Delete
```

---

## Gmail

```text
Trash

↓

30 days

↓

Permanent Delete
```

---

## E-commerce

Orders:

```text
Never Delete
```

---

## Audit Logs

```text
Keep

7 years
```

Depends on regulations.

---

# Cascading Soft Delete

Suppose:

Delete:

```text
User
```

Should we delete:

```text
Posts?

Comments?

Likes?
```

Business decision.

Possible strategies:

---

## Option 1

Keep everything.

Show:

```text
Deleted User
```

Common on forums.

---

## Option 2

Soft delete everything.

```text
User

↓

Posts

↓

Comments
```

---

## Option 3

Anonymize.

Replace:

```text
Rahul
```

with:

```text
Deleted User
```

Popular for privacy.

---

# Real-World Example

Suppose:

Delete Course.

Should lessons disappear?

Depends.

Maybe:

```text
Course

↓

Deleted
```

Lessons:

Still exist.

Hidden.

---

# Query Design

Without soft delete:

```javascript
findById(id)
```

With soft delete:

```javascript
findOne({

_id:id,

deletedAt:null

})
```

Every repository method should automatically exclude deleted records.

---

# Repository Pattern Example

Instead of:

```javascript
find()
```

Repository always performs:

```javascript
find({

deletedAt:null

})
```

Controllers never need to remember this.

Excellent architecture.

---

# Soft Delete vs Archive

These are different.

Archive:

```text
Still active

Rarely accessed
```

Deleted:

```text
User removed it.
```

Example:

Blog.

States:

```text
Draft

Published

Archived

Deleted
```

All different meanings.

---

# Common Beginner Mistakes

## Mistake 1

Hard deleting important data.

Bad:

```javascript
deleteOne()
```

---

## Mistake 2

Forgetting to filter deleted records.

Users suddenly see deleted posts.

Always filter them.

---

## Mistake 3

Using only:

```javascript
isDeleted
```

Without:

```text
deletedAt
```

Now you don't know when deletion happened.

---

## Mistake 4

Never cleaning soft-deleted data.

Eventually:

Millions of deleted records.

Need cleanup policies.

---

## Mistake 5

Soft deleting everything.

Temporary data like:

- OTP
    
- Sessions
    
- Cache
    
- Verification tokens
    

usually doesn't need soft delete.

---

# Best Practices

- Use soft delete for important business data.
    
- Store `deletedAt` instead of only `isDeleted` when possible.
    
- Consider storing `deletedBy` for auditability.
    
- Update repository queries to exclude deleted records by default.
    
- Provide a restore feature where appropriate.
    
- Run scheduled cleanup jobs for temporary soft-deleted data.
    
- Decide cascade behavior based on business requirements.
    

---

# Soft Delete Checklist

For every entity, ask:

```text
Is this data important?

Can users accidentally delete it?

Will someone need to restore it?

Do legal or business requirements require keeping it?

Should deleted data remain hidden or recoverable?

When should permanently deleted records be cleaned up?

Should related entities also be deleted?
```

---

# Real Backend Example

Suppose you're building a **Learning Management System**.

Entities:

```text
Course

Lesson

Assignment

Submission
```

Soft Delete Policy:

|Entity|Strategy|
|---|---|
|Course|Soft Delete|
|Lesson|Soft Delete|
|Assignment|Soft Delete|
|Submission|Usually Never Delete (important academic record)|

Repository:

```javascript
find({

deletedAt:null

})
```

Admin:

```text
View Deleted Courses

↓

Restore

↓

Permanent Delete (after 90 days)
```

This provides a safe and user-friendly deletion workflow.

---

# Module 14 Summary

By the end of this module, you should be able to:

- Explain the difference between hard delete and soft delete.
    
- Decide which entities require soft delete.
    
- Choose between `status`, `isDeleted`, and `deletedAt` strategies.
    
- Design restore and cleanup workflows.
    
- Update queries to ignore deleted records by default.
    
- Plan cascade deletion and retention policies based on business requirements.
    
- Integrate soft delete cleanly into your repository layer.
    

---

# Mini Exercise

Design the deletion strategy for a **Hospital Management System**.

Entities:

```text
Patient

Doctor

Appointment

Prescription

MedicalRecord

Invoice
```

For each entity:

1. Should it use hard delete or soft delete?
    
2. If soft delete, which fields would you add (`status`, `deletedAt`, `deletedBy`)?
    
3. Should users be able to restore it?
    
4. Should there be an automatic cleanup policy?
    
5. What should happen to related entities when one entity is deleted?
    

> **Next Module:** **Module 15 — Audit Fields**, where you'll learn how to track **who created, updated, deleted, or restored data**, enabling accountability, debugging, compliance, and powerful administrative features in production backend systems.