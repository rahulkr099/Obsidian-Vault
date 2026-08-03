# Module 12 — Index Design

> **Goal:** Learn how to design indexes from application queries, not by guesswork, so your backend remains fast as your data grows.

---

# Why This Module Matters

This is one of the most valuable backend engineering skills.

Many developers know how to create an index.

Very few know **when**, **where**, and **why** to create one.

A professional backend engineer never asks:

> **"Which fields should I index?"**

Instead, they ask:

> **"Which queries need to be fast?"**

Indexes are designed for **queries**, not for fields.

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
Index Design   ← You are here
      ↓
API Design
      ↓
Implementation
```

Notice something important:

We studied **queries in Module 2**.

Now those queries finally become useful.

---

# What Is an Index?

Think of a book.

Without an index:

```text
Open book

↓

Read page 1

↓

Read page 2

↓

Read page 3

↓

...

↓

Find Chapter 12
```

Very slow.

---

With an index:

```text
Index

↓

Chapter 12

↓

Page 328
```

Immediately.

A database index works exactly the same way.

Instead of scanning every document,

the database jumps directly to the required records.

---

# Without an Index

Suppose your User collection has:

```text
10 users
```

Finding Rahul:

```text
User1

↓

User2

↓

User3

↓

...

↓

Rahul
```

Not a problem.

---

Now imagine:

```text
50 million users
```

Without an index,

every search becomes expensive.

---

# With an Index

Create an index on:

```text
email
```

Now:

```text
Find email

↓

Index

↓

Record
```

Milliseconds.

---

# Important Rule

> **Indexes speed up reads but slow down writes.**

Why?

Whenever data changes,

the database must also update the index.

Example:

Insert User

```text
Save document

↓

Update email index

↓

Update username index
```

More indexes = more work during inserts and updates.

---

# Engineering Mindset

Never ask:

```text
Should I index email?
```

Ask:

```text
Which queries happen most often?
```

---

# Step 1 — Start From Queries

Suppose your Blog App has these APIs:

```http
GET /posts
```

Shows latest posts.

---

```http
GET /posts/:slug
```

Find by slug.

---

```http
GET /users/:username
```

Find user.

---

```http
GET /posts?author=Rahul
```

Find author's posts.

---

Immediately you can identify candidate indexes.

---

# Step 2 — Identify Frequent Queries

Example:

Homepage:

```text
Latest Posts
```

Runs:

```text
500,000 times/day
```

Needs optimization.

---

Admin Report:

```text
Monthly statistics
```

Runs:

```text
1 time/day
```

Probably doesn't need a special index.

Always optimize frequent queries first.

---

# Types of Indexes

The most common indexes are:

```text
Single Field

Compound

Unique

Text

TTL

Sparse

Partial

Geospatial
```

Let's study each one.

---

# 1. Single Field Index

Index on one field.

Example:

```text
email
```

Query:

```javascript
findOne({
    email:
    "rahul@gmail.com"
})
```

Index:

```text
email
```

Very common.

---

Examples:

```text
username

slug

shortCode

sku
```

---

# 2. Compound Index

Index multiple fields together.

Example:

Homepage query:

```text
status

publishedAt
```

Query:

```javascript
find({

status: "published"

})

.sort({

publishedAt:-1

})
```

Best index:

```text
(status, publishedAt)
```

This is much better than two separate indexes.

---

# Another Example

Search posts by author.

Newest first.

Query:

```javascript
find({

author: userId

})

.sort({

createdAt:-1

})
```

Index:

```text
(author, createdAt)
```

---

# Compound Index Order Matters

Example:

Index:

```text
(author, createdAt)
```

Good:

```javascript
author

↓

createdAt
```

Good:

```javascript
author only
```

Bad:

```javascript
createdAt only
```

The order is extremely important.

---

# 3. Unique Index

Guarantees uniqueness.

Example:

```text
email
```

Unique index.

---

Example:

```text
slug
```

Unique.

---

Example:

```text
shortCode
```

Unique.

---

# 4. Text Index

Used for searching text.

Example:

Search:

```text
MongoDB Indexes
```

Query:

```javascript
$text
```

Index:

```text
title

content
```

Perfect for:

- Blogs
    
- Documentation
    
- Notes
    
- Articles
    

---

# 5. TTL Index

TTL = Time To Live

Automatically deletes expired documents.

Example:

Password reset token.

```text
Expires

↓

15 minutes
```

Database removes it automatically.

---

Other examples:

```text
OTP

Sessions

Temporary tokens

Cache
```

Very useful.

---

# 6. Sparse Index

Indexes only documents that contain a field.

Example:

```text
middleName
```

Many users don't have it.

Sparse index ignores missing values.

---

# 7. Partial Index

Indexes only documents matching a condition.

Example:

Only published posts.

```text
status

↓

published
```

Smaller index.

Better performance.

---

# 8. Geospatial Index

For location queries.

Example:

Ride Sharing.

```text
Drivers

↓

Nearby
```

Food delivery.

```text
Restaurants

↓

Near me
```

Maps.

Real estate.

---

# Real Blog Example

Query:

Homepage.

```javascript
find({

status:"published"

})

.sort({

publishedAt:-1

})
```

Index:

```text
(status, publishedAt)
```

---

Query:

```javascript
findOne({

slug:"mongodb-guide"

})
```

Index:

```text
slug
```

---

Query:

```javascript
find({

author:userId

})
```

Index:

```text
author
```

---

Query:

Search.

```javascript
$text
```

Index:

```text
title

content
```

---

# URL Shortener Example

Most frequent query:

```javascript
findOne({

shortCode:"abc123"

})
```

Index:

```text
shortCode
```

Without it,

every redirect becomes slow.

---

Analytics:

```javascript
find({

shortURL:id

})
```

Index:

```text
shortURL
```

---

# Todo Application

Queries:

```text
My Todos
```

Index:

```text
userId
```

---

Completed Todos:

```text
userId

status
```

Compound:

```text
(userId, status)
```

---

Sort:

```text
dueDate
```

Index:

```text
(userId, dueDate)
```

---

# E-commerce

Search:

```text
Category
```

Index:

```text
category
```

---

Product page:

```text
slug
```

Index:

```text
slug
```

---

Latest products.

```text
createdAt
```

Index:

```text
(createdAt)
```

---

Orders:

```text
customerId

createdAt
```

Compound.

---

# Learning Management System

Query:

```text
Student Courses
```

Index:

```text
studentId
```

---

Query:

```text
Course Lessons
```

Index:

```text
courseId
```

---

Query:

```text
Teacher Courses
```

Index:

```text
teacherId
```

---

# Indexes for Relationships

Suppose:

Comment

```text
postId
```

Query:

```javascript
find({

postId

})
```

Index:

```text
postId
```

Always index foreign/reference fields that are frequently queried.

---

# When NOT to Create an Index

Don't index:

Rarely queried fields.

Example:

```text
bio
```

If nobody searches by bio,

no index needed.

---

Don't index:

Tiny collections.

Example:

```text
10 categories
```

Full scan is already fast.

---

Don't index:

Fields that change constantly unless necessary.

Frequent updates increase index maintenance cost.

---

# Measuring Performance

Never guess.

Use:

```javascript
explain()
```

MongoDB:

```javascript
db.posts.find({

status:"published"

}).explain()
```

Shows:

- Index used
    
- Documents scanned
    
- Execution time
    

Always measure.

---

# Common Beginner Mistakes

## Mistake 1

Indexing every field.

Wrong.

Indexes consume:

- RAM
    
- Disk
    
- Write performance
    

---

## Mistake 2

Ignoring query patterns.

Indexes exist to speed up queries.

No query.

No index.

---

## Mistake 3

Wrong compound index order.

Example:

Query:

```text
author

↓

createdAt
```

Wrong index:

```text
(createdAt, author)
```

Correct:

```text
(author, createdAt)
```

---

## Mistake 4

Not indexing foreign keys (references).

Example:

```text
postId

userId

authorId

courseId
```

These are queried frequently.

---

## Mistake 5

Never checking query performance.

Always verify using:

- MongoDB `explain()`
    
- PostgreSQL `EXPLAIN ANALYZE`
    
- MySQL `EXPLAIN`
    

---

# Index Design Checklist

For every query, ask:

```text
Which field is filtered?

Which field is sorted?

Is pagination used?

How often does this query run?

Does this query need a compound index?

Can a text index help?

Will a unique index prevent duplicates?

Will this index slow down writes too much?
```

---

# Blog Application Index Plan

|Query|Recommended Index|
|---|---|
|Login by email|`(email)` Unique|
|Profile by username|`(username)` Unique|
|Blog by slug|`(slug)` Unique|
|Homepage|`(status, publishedAt)`|
|Author posts|`(author, createdAt)`|
|Comments for post|`(postId, createdAt)`|
|Search|`Text(title, content)`|
|Like lookup|`(userId, postId)` Unique Compound|

Notice how **every index comes directly from a query**, not from random guessing.

---

# Best Practices

- Design indexes **after** identifying queries.
    
- Optimize high-frequency reads first.
    
- Use compound indexes for filtering + sorting.
    
- Keep the number of indexes reasonable.
    
- Index reference fields that are queried often.
    
- Measure query performance before and after adding indexes.
    
- Remove unused indexes over time.
    

---

# Module 12 Summary

By the end of this module, you should be able to:

- Explain what indexes are and why they improve query performance.
    
- Design indexes based on real application queries.
    
- Choose between single-field, compound, unique, text, TTL, and other index types.
    
- Understand how compound index order affects performance.
    
- Recognize the trade-off between faster reads and slower writes.
    
- Use query analysis tools like `explain()` to verify index effectiveness.
    

---

# Mini Exercise

Design an index strategy for a **Job Portal**.

Entities:

```text
User

Company

Job

Application
```

Requirements:

```text
Users search jobs by title and location.
Users filter jobs by salary and experience.
Companies view their posted jobs.
Recruiters view applications sorted by newest.
Users save jobs.
Admins search users by email.
Expired jobs should disappear automatically.
```

For each requirement:

1. Write the expected query.
    
2. Identify the filter fields.
    
3. Identify the sort fields.
    
4. Choose the best index (single, compound, text, unique, TTL, etc.).
    
5. Explain why that index is appropriate.
    
6. Decide whether any indexes are unnecessary.
    

> **Next Module:** **Module 13 — Think About Growth**, where you'll learn how to design databases and APIs that work not only for **100 users**, but also for **1 million users**, without over-engineering from the start.