# Module 11 — Database Constraints

> **Goal:** Learn how to use the database itself to protect your data by enforcing rules that your application cannot accidentally bypass.

---

# Why This Module Matters

Imagine your backend has a bug.

Your validation middleware misses a case.

Your service layer has an error.

Should your database still protect your data?

**Yes.**

This is exactly why database constraints exist.

A professional backend engineer follows this rule:

> **Never trust application code alone. Let the database enforce important rules.**

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
Primary Keys
      ↓
Attributes
      ↓
Normalization
      ↓
State Modeling
      ↓
Validation
      ↓
Database Constraints   ← You are here
      ↓
Indexes
```

Notice something important.

Validation checks input.

**Constraints protect stored data.**

---

# What is a Database Constraint?

A constraint is a rule enforced by the database.

Example:

```text
Every email must be unique.
```

Even if two requests arrive at the exact same time,

the database guarantees that only one succeeds.

Without constraints:

```text
User A

↓

rahul@gmail.com
```

and

```text
User B

↓

rahul@gmail.com
```

Both could be saved.

Your application becomes inconsistent.

---

# Why Application Validation Is Not Enough

Imagine this flow:

```text
Request A
        ↓
Email doesn't exist
```

At the same time:

```text
Request B
        ↓
Email doesn't exist
```

Both continue.

Both save.

Now you have duplicate emails.

This is called a **race condition**.

Only the database can prevent it reliably.

---

# Types of Database Constraints

The most common constraints are:

```text
Primary Key

Unique

Foreign Key (SQL)

Check

Not Null

Default

Compound Unique
```

Let's study each one.

---

# 1. Primary Key Constraint

Every table or collection needs an identity.

MongoDB:

```text
_id
```

Automatically unique.

PostgreSQL:

```sql
PRIMARY KEY
```

Example:

```text
User

↓

_id
```

No two users can have the same `_id`.

---

# 2. Unique Constraint

Most commonly used constraint.

Example:

```text
Email
```

Only one user can own:

```text
rahul@gmail.com
```

Database:

```text
Unique
```

If another user tries:

Database rejects it.

---

## Real Examples

### User

```text
email

username
```

Unique.

---

### Product

```text
SKU
```

Unique.

---

### Blog

```text
slug
```

Unique.

---

### URL Shortener

```text
shortCode
```

Unique.

---

# 3. Compound Unique Constraint

Sometimes one field isn't enough.

Example:

Users like posts.

Question:

Can Rahul like the same post twice?

No.

Need uniqueness on:

```text
UserId

+

PostId
```

Not individually.

Together.

Example:

```text
(UserId, PostId)
```

Only one record allowed.

---

## More Examples

### Student Enrollment

```text
(StudentId, CourseId)
```

A student cannot enroll in the same course twice.

---

### Shopping Cart

```text
(UserId, ProductId)
```

Prevent duplicate cart items.

---

### Follow System

```text
(FollowerId, FollowingId)
```

Prevent duplicate follows.

---

# 4. Not Null Constraint

Some fields must always exist.

Example:

```text
User

email
```

Cannot be:

```text
NULL
```

Another example:

```text
Order

customerId
```

Must exist.

---

Fields often marked NOT NULL:

```text
email

password

title

price

authorId
```

---

# 5. Default Constraint

Sometimes the database should assign a value.

Example:

New post.

Status:

```text
draft
```

No need for the application to send it.

Database default:

```text
status = draft
```

---

Examples:

```text
views = 0

likesCount = 0

createdAt = current timestamp

status = pending
```

Defaults simplify your backend.

---

# 6. Check Constraint (Mostly SQL)

Ensures values satisfy a rule.

Example:

Age:

```text
Age >= 18
```

Price:

```text
Price > 0
```

Rating:

```text
Rating BETWEEN 1 AND 5
```

MongoDB doesn't have native CHECK constraints like PostgreSQL, so these rules are usually enforced through schema validation or application logic.

---

# 7. Foreign Key Constraint (SQL)

Suppose:

```text
Comment

↓

Post
```

Question:

Can a comment reference a post that doesn't exist?

No.

SQL solves this using:

```text
Foreign Key
```

The database rejects invalid references.

---

### MongoDB Equivalent

MongoDB doesn't enforce foreign keys.

Instead:

Application validates:

```text
Does postId exist?
```

before inserting the comment.

This is why service-layer validation is important in MongoDB.

---

# Constraints in MongoDB

Although MongoDB is schema-flexible,

Mongoose lets us define constraints.

Example:

```javascript
email: {
    type: String,
    required: true,
    unique: true
}
```

Status:

```javascript
status: {
    type: String,
    enum: [
        "draft",
        "published",
        "archived"
    ]
}
```

Remember:

`unique: true` creates a unique index.

It is **not** a validator.

---

# Example — Blog Application

## User

Constraints:

```text
_id

Primary Key

email

Unique

username

Unique

password

Required
```

---

## Post

Constraints:

```text
_id

Primary Key

slug

Unique

title

Required

authorId

Required

status

Enum

Default = draft
```

---

## Comment

Constraints:

```text
_id

Primary Key

postId

Required

authorId

Required

content

Required
```

---

## Like

Constraints:

```text
(UserId, PostId)

Compound Unique
```

Now duplicate likes become impossible.

---

# Example — URL Shortener

Fields:

```text
shortCode
```

Constraint:

```text
Unique
```

Because:

```text
abc123
```

must always point to one URL.

---

# Example — E-commerce

Product

```text
SKU

↓

Unique
```

Price:

```text
> 0
```

Stock:

```text
>= 0
```

Order:

```text
customerId

↓

Required
```

---

# Example — Learning Management System

Enrollment:

```text
StudentId

CourseId
```

Constraint:

```text
Unique Compound
```

Student cannot enroll twice.

---

Course:

```text
courseCode
```

Unique.

---

# Constraints vs Validation

Many beginners confuse these.

## Validation

Purpose:

```text
Reject bad requests.
```

Example:

```text
Email format invalid.
```

---

## Constraint

Purpose:

```text
Protect stored data.
```

Example:

```text
Duplicate email.
```

---

Both are required.

Professional systems use both.

---

# Handling Constraint Errors

Suppose:

Two users register using:

```text
rahul@gmail.com
```

Database rejects one.

Return:

```json
{
  "success": false,
  "message": "Email already exists."
}
```

Don't expose raw database errors to users.

---

# Common Beginner Mistakes

## Mistake 1

Checking uniqueness only in code.

Wrong:

```text
Find email

↓

Insert
```

Race conditions can still occur.

Always add a unique constraint.

---

## Mistake 2

Making every field unique.

Wrong:

```text
Name

↓

Unique
```

Many people can have the same name.

Think carefully.

---

## Mistake 3

Ignoring compound uniqueness.

Example:

```text
Like
```

Needs:

```text
(UserId, PostId)
```

Not just:

```text
UserId
```

---

## Mistake 4

Using constraints instead of validation.

Constraints are the last safety net.

Validation should happen before reaching the database.

---

## Mistake 5

Forgetting defaults.

Example:

```text
views = 0
```

Much simpler than checking:

```javascript
if (!views)
```

everywhere.

---

# Real Backend Example

Imagine a **Task Management System**.

Task:

```text
_id

title

status

projectId

assigneeId

createdAt
```

Constraints:

```text
_id

↓

Primary Key
```

```text
title

↓

Required
```

```text
status

↓

Enum

↓

todo

in_progress

done
```

```text
createdAt

↓

Default

Current Time
```

The database guarantees these rules even if your backend has bugs.

---

# Best Practices

- Use primary keys for identity.
    
- Add unique constraints to business identifiers.
    
- Use compound unique constraints for many-to-many relationships.
    
- Make important fields non-null.
    
- Use sensible default values.
    
- Validate in your application **and** enforce constraints in the database.
    
- Handle constraint errors gracefully.
    

---

# Database Constraint Checklist

For every entity, ask:

```text
Does every record have a primary key?

Which fields must be unique?

Which combinations must be unique?

Which fields cannot be null?

Which fields need default values?

Are enum values restricted?

Will the database protect against duplicate records?
```

If the answer is **yes**, your data integrity is much stronger.

---

# Module 11 Summary

By the end of this module, you should be able to:

- Explain why database constraints are essential.
    
- Distinguish validation from database constraints.
    
- Choose appropriate primary key, unique, compound unique, not-null, default, and enum constraints.
    
- Understand the role of foreign keys in SQL and application-level reference validation in MongoDB.
    
- Protect your application from race conditions and duplicate data.
    
- Design schemas that remain consistent even when application code fails.
    

---

# Mini Exercise

Design the database constraints for an **Online Banking System**.

Entities:

```text
User

BankAccount

Transaction

Beneficiary

Card
```

For each entity:

1. Identify the primary key.
    
2. Decide which fields should be unique.
    
3. Identify any compound unique constraints.
    
4. List required (non-null) fields.
    
5. Decide appropriate default values.
    
6. Identify any enum constraints.
    
7. Think about which relationships would use foreign keys (SQL) or application-level validation (MongoDB).
    

> **Next Module:** **Module 12 — Index Design**, where you'll learn one of the most valuable backend engineering skills: designing indexes based on real application queries to make your APIs fast without wasting memory or slowing down writes.