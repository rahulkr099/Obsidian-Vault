# Module 5 — Decide Relationships

> **Goal:** Learn how to identify and model relationships between entities using **One-to-One (1:1)**, **One-to-Many (1:N)**, and **Many-to-Many (M:N)** relationships.

---

# Why This Module Matters

You already know:

```text
Requirements
        ↓
User Stories
        ↓
Queries
        ↓
Entities
        ↓
ER Diagram
```

Now comes one of the most important database design decisions:

> **How many objects can be related to each other?**

Choosing the wrong relationship can make your database difficult to maintain and slow to query.

---

# The Engineering Flow

```text
Requirements
        ↓
Queries
        ↓
Entities
        ↓
ER Diagram
        ↓
Relationship Types   ← You are here
        ↓
Schema Design
```

---

# What Is a Relationship?

A relationship describes how two entities are connected.

Example:

```text
User
   |
writes
   |
Post
```

Now ask:

> Can one user write many posts?

Yes.

> Can one post have many authors?

Maybe, depending on the business.

This is how relationship types are discovered.

---

# The Three Main Relationship Types

```text
1. One-to-One (1:1)

2. One-to-Many (1:N)

3. Many-to-Many (M:N)
```

Let's study each one.

---

# Part 1 — One-to-One (1:1)

One record in Entity A is related to exactly one record in Entity B.

Example:

```text
User
    |
has
    |
Profile
```

```text
One User
        ↓
One Profile
```

Diagram:

```text
+------+        +---------+
| User | 1 ─── 1| Profile |
+------+        +---------+
```

---

## Real-World Examples

### Passport System

```text
Person
    |
owns
    |
Passport
```

Usually:

```text
1 Person
↓

1 Passport
```

---

### Employee

```text
Employee
     |
has
     |
Payroll Account
```

---

### Medical System

```text
Patient
     |
has
     |
Medical Record
```

---

## When to Use 1:1

Use it when:

- Extra information belongs to exactly one parent.
    
- You want to separate optional or sensitive data.
    

Example:

Instead of:

```text
User

name

email

bio

avatar

address

preferences

socialLinks

theme

language
```

You can split it:

```text
User

↓

UserProfile
```

This keeps the main table smaller.

---

# Part 2 — One-to-Many (1:N)

One record is related to many records.

This is the most common relationship.

Example:

```text
User

↓

writes

↓

Post
```

One user:

```text
Rahul
```

can write:

```text
Post A

Post B

Post C
```

Each post belongs to one author.

Diagram:

```text
+------+      +------+
| User |1 ───<| Post |
+------+      +------+
```

---

## More Examples

### Blog

```text
Post

↓

has

↓

Comments
```

One post:

```text
↓

Comment 1

Comment 2

Comment 3
```

---

### Course

```text
Course

↓

contains

↓

Lessons
```

---

### Customer

```text
Customer

↓

places

↓

Orders
```

---

### Restaurant

```text
Restaurant

↓

offers

↓

Menu Items
```

---

# Identifying 1:N

Ask:

> Can one parent have many children?

If yes:

It's probably **One-to-Many**.

Examples:

```text
Teacher

↓

Courses
```

```text
Company

↓

Employees
```

```text
Department

↓

Students
```

---

# Part 3 — Many-to-Many (M:N)

This relationship confuses beginners the most.

Example:

Students and Courses.

Question:

Can one student enroll in many courses?

Yes.

Can one course have many students?

Also yes.

Diagram:

```text
Student

↔

Course
```

This is **Many-to-Many**.

---

## Important Rule

A Many-to-Many relationship usually needs a **junction (bridge) entity**.

Instead of:

```text
Student

↔

Course
```

Create:

```text
Student

↓

Enrollment

↓

Course
```

Diagram:

```text
+---------+       +------------+       +--------+
| Student |1 ───< | Enrollment |>─── 1 | Course |
+---------+       +------------+       +--------+
```

---

# More M:N Examples

## User Likes Post

Question:

Can one user like many posts?

Yes.

Can one post be liked by many users?

Yes.

Need:

```text
Like
```

Diagram:

```text
User

↓

Like

↓

Post
```

---

## Product and Order

Can one order contain many products?

Yes.

Can one product appear in many orders?

Yes.

Need:

```text
OrderItem
```

Diagram:

```text
Order

↓

OrderItem

↓

Product
```

---

## Movie Platform

Actors

↓

MovieCast

↓

Movie

---

# Relationship Comparison

|Relationship|Example|
|---|---|
|One-to-One|User → Profile|
|One-to-Many|User → Posts|
|Many-to-Many|Student ↔ Course|

---

# Step-by-Step Process

Whenever you see two entities:

Ask three questions.

---

## Question 1

Can one A have many B?

Example:

```text
User

↓

Posts
```

Answer:

Yes.

---

## Question 2

Can one B have many A?

Example:

```text
Post

↓

Authors
```

Answer:

Usually no.

Result:

```text
One-to-Many
```

---

Another example:

Student

↓

Courses

Yes.

Course

↓

Students

Yes.

Result:

```text
Many-to-Many
```

---

# Real Example — Blog

Entities:

```text
User

Post

Comment

Category

Tag

Like
```

Relationships:

```text
User

↓

writes

↓

Post

(1:N)
```

---

```text
Post

↓

has

↓

Comment

(1:N)
```

---

```text
Category

↓

contains

↓

Post

(1:N)
```

---

```text
User

↓

likes

↓

Post

(M:N)

↓

Need Like entity
```

---

```text
Post

↓

has

↓

Tag

(M:N)

↓

Need PostTag entity (SQL)

or

Array of references (MongoDB)
```

---

# Real Example — E-commerce

Entities:

```text
Customer

Order

OrderItem

Product

Category
```

Relationships:

```text
Customer

↓

Orders

1:N
```

---

```text
Order

↓

OrderItems

1:N
```

---

```text
Product

↓

Category

N:1
```

---

```text
Order

↓

Product

M:N

↓

OrderItem
```

---

# Self Relationships

Sometimes an entity relates to itself.

Example:

Followers.

```text
User

↓

follows

↓

User
```

Question:

Can Rahul follow many users?

Yes.

Can many users follow Rahul?

Yes.

This is:

```text
Many-to-Many
```

Implemented using:

```text
Follow
```

---

Another example:

```text
Employee

↓

manages

↓

Employee
```

One manager.

Many employees.

That's a self **One-to-Many**.

---

# How Queries Help Decide Relationships

Suppose you have these queries:

```text
Show all posts by Rahul.
```

Immediately tells you:

```text
User

↓

Posts

1:N
```

---

Query:

```text
Show students enrolled in React course.
```

Means:

```text
Student

↓

Enrollment

↓

Course
```

---

Query:

```text
Show all products in Order #123.
```

Means:

```text
Order

↓

OrderItem

↓

Product
```

Queries often reveal relationships naturally.

---

# Common Beginner Mistakes

## Mistake 1

Ignoring Many-to-Many.

Wrong:

```text
Student

↓

Course
```

Correct:

```text
Student

↓

Enrollment

↓

Course
```

---

## Mistake 2

Creating arrays everywhere.

Wrong:

```javascript
User

posts: []

comments: []

likes: []

followers: []

following: []
```

Large arrays become difficult to manage and query.

---

## Mistake 3

Confusing roles with entities.

Wrong:

```text
Teacher

Student
```

When both are actually:

```text
User

↓

role
```

Sometimes one entity with a role field is enough.

---

## Mistake 4

Choosing relationships without checking requirements.

Always go back to the business rules.

---

## Mistake 5

Thinking relationship decisions are database-specific.

Whether you use:

- MongoDB
    
- PostgreSQL
    
- MySQL
    
- SQL Server
    

The **business relationship stays the same**.

Only the implementation changes.

---

# Best Practices

- Decide relationships before creating schemas.
    
- Use business rules, not guesses.
    
- Ask "How many?" for every relationship.
    
- Introduce junction entities for Many-to-Many relationships.
    
- Review relationships using real application queries.
    
- Keep the model simple and business-focused.
    

---

# Module 5 Summary

By the end of this module, you should be able to:

- Identify One-to-One, One-to-Many, and Many-to-Many relationships.
    
- Ask the right questions to determine relationship cardinality.
    
- Recognize when a junction entity (such as `Enrollment`, `Like`, or `OrderItem`) is needed.
    
- Model self-relationships like followers or managers.
    
- Use application queries to validate your relationship decisions before designing the database.
    

---

# Mini Exercise

Design the relationships for a **Job Portal**.

Requirements:

```text
Users can apply for jobs.
Companies post jobs.
Recruiters manage job postings.
Users can save jobs.
Companies receive applications.
Users can upload resumes.
Recruiters review applications.
```

### Your Tasks

1. List the entities.
    
2. Identify every relationship.
    
3. Decide whether each relationship is:
    
    - One-to-One
        
    - One-to-Many
        
    - Many-to-Many
        
4. Identify any junction entities (for example, `Application` or `SavedJob`).
    
5. Draw a simple ER diagram with relationship types.
    

> **Next Module:** **Module 6 — Choose the Primary Key**, where you'll learn how to uniquely identify every entity, design natural vs. surrogate keys, and decide when to use `_id`, UUIDs, slugs, composite keys, and unique business identifiers.