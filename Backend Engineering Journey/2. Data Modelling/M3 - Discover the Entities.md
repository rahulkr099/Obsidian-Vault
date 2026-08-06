# Module 3 — Discover the Entities

> **Goal:** Learn how to identify the core business objects (entities) of your application before designing fields, relationships, or database schemas.

---

# Why This Module Matters

After Module 2, you know **what queries your application needs to answer**.

Now ask:

> **"What things (objects) exist in this system?"**

These "things" are called **entities**.

Eventually, most entities become:

- MongoDB Collections
    
- PostgreSQL Tables
    
- MySQL Tables
    

But don't think about databases yet.

Think about the **business**.

---

# The Engineering Flow

```text
Business Requirements
        ↓
User Stories
        ↓
Queries
        ↓
Entities   ← You are here
        ↓
Relationships
        ↓
Schema Design
```

---

# What Is an Entity?

An entity is something that has:

- An identity
    
- Its own data
    
- A lifecycle
    
- Independent existence
    

Examples:

```text
User

Post

Comment

Product

Order

Course

Student
```

These are all entities because they represent real business objects.

---

# Step 1 — Read the Requirements Again

Example:

```text
Users can create blog posts.

Users can comment.

Users can like posts.

Users can follow authors.

Admins can remove posts.
```

Don't think about collections.

Instead, ask:

> What objects are being discussed?

---

# Step 2 — Find the Nouns

One of the easiest techniques.

Requirement:

```text
Users create blog posts.
```

Nouns:

```text
User

Post
```

Requirement:

```text
Users comment on posts.
```

Nouns:

```text
User

Comment

Post
```

Requirement:

```text
Users follow authors.
```

Nouns:

```text
User

Author
```

But wait...

Is **Author** a separate entity?

No.

An author is simply a **User** who has published posts.

So we don't create a separate Author collection.

---

# Step 3 — Remove Duplicates

Example:

Requirements mention:

```text
User

Author

Writer

Member
```

Ask:

Are these different things?

Maybe not.

Often they all represent:

```text
User
```

One entity.

Different roles.

---

# Step 4 — Identify Independent Objects

Ask:

Can this object exist by itself?

Example:

### User

Yes.

Independent.

---

### Post

Yes.

Independent.

---

### Comment

Yes.

Independent.

---

### Like

Maybe.

Depends on the design.

We'll discuss that later.

---

### Login

No.

It is an action.

Not an entity.

---

### Search

No.

It is a feature.

Not an entity.

---

# Step 5 — Ignore Actions

Many beginners mistake actions for entities.

Wrong:

```text
Login

Logout

Register

Publish

Delete
```

These are operations.

Not business objects.

Entities are usually nouns.

Actions become APIs or service methods.

---

# Step 6 — Ignore Database Thinking

Don't think:

```text
Should I embed?

Should I reference?
```

Too early.

First discover the entities.

Nothing else.

---

# Example 1 — Blog Application

Requirements:

```text
Users write posts.

Posts have comments.

Users like posts.

Posts belong to categories.

Posts have tags.
```

Entities:

```text
User

Post

Comment

Category

Tag

Like
```

Nothing more.

No fields yet.

---

# Example 2 — E-Commerce

Requirements:

```text
Customers buy products.

Products belong to categories.

Customers add products to cart.

Customers place orders.

Customers write reviews.
```

Entities:

```text
Customer

Product

Category

Cart

Order

Review
```

Notice we still haven't created fields.

---

# Example 3 — Library Management

Requirements:

```text
Students borrow books.

Librarians issue books.

Books belong to categories.

Students reserve books.

Students pay fines.
```

Entities:

```text
Student

Book

Category

BorrowRecord

Reservation

Fine

Librarian
```

---

# Example 4 — Learning Management System

Requirements:

```text
Teachers create courses.

Courses contain lessons.

Students enroll.

Students take quizzes.

Students submit assignments.
```

Entities:

```text
Teacher

Student

Course

Lesson

Enrollment

Quiz

Assignment

Submission
```

---

# Step 7 — Merge Similar Entities

Sometimes beginners create too many collections.

Wrong:

```text
PublishedPost

DraftPost

ArchivedPost
```

Correct:

```text
Post
```

Use:

```text
status

↓

draft

published

archived
```

One entity.

Different states.

---

# Step 8 — Find Hidden Entities

Some entities are not obvious.

Example:

```text
Users follow users.
```

Question:

How do we store follows?

Eventually:

```text
Follow
```

becomes an entity.

Another example:

```text
Users like posts.
```

Usually:

```text
Like
```

becomes an entity.

These are called **relationship entities** or **junction entities**.

---

# Step 9 — Think About Ownership

Ask:

Who owns this entity?

Example:

```text
User

↓

owns

↓

Post
```

Another:

```text
Post

↓

owns

↓

Comment
```

Ownership helps you understand future relationships.

---

# Step 10 — Avoid Premature Optimization

Don't ask:

```text
Should Likes be embedded?

Should Comments be embedded?
```

That belongs in Module 8.

Right now, simply identify them.

---

# Entity Checklist

For every possible entity, ask:

```text
Does it have its own identity?

Does it store its own data?

Can it exist independently?

Does it have its own lifecycle?

Will it likely become a collection/table?
```

If the answer is mostly yes,

it's probably an entity.

---

# Blog Application Walkthrough

Requirements:

```text
Users register.

Users write posts.

Users edit posts.

Users comment.

Users like posts.

Users follow users.

Admins remove posts.
```

Entities:

```text
User

Post

Comment

Like

Follow
```

Notice:

We did **not** create:

```text
Register

Login

Publish

Delete

Search
```

Those are actions.

---

# URL Shortener Example

Requirements:

```text
Users shorten URLs.

Users create custom aliases.

Users view analytics.

Users manage links.
```

Entities:

```text
User

ShortURL

ClickEvent
```

Why ClickEvent?

Because every click has:

- timestamp
    
- browser
    
- device
    
- IP
    
- country
    
- referrer
    

Each click is its own business object.

---

# Chat Application Example

Requirements:

```text
Users send messages.

Users create groups.

Users join groups.

Users upload media.
```

Entities:

```text
User

Conversation

Message

Group

Membership

Attachment
```

Notice that:

```text
Send
Join
Upload
```

are actions.

---

# Expense Tracker Example

Requirements:

```text
Users add income.

Users add expenses.

Users create categories.

Users generate reports.
```

Entities:

```text
User

Transaction

Category
```

Not:

```text
Income

Expense
```

Instead:

```text
Transaction

↓

type

income

expense
```

One entity.

Two types.

---

# Common Beginner Mistakes

## Mistake 1

Creating entities from verbs.

Wrong:

```text
Login

Publish

Search
```

Correct:

```text
User

Post

Comment
```

---

## Mistake 2

Creating separate entities for states.

Wrong:

```text
DraftPost

PublishedPost

DeletedPost
```

Correct:

```text
Post

↓

status
```

---

## Mistake 3

Ignoring hidden entities.

Example:

```text
Users like posts.
```

Needs:

```text
Like
```

---

## Mistake 4

Creating entities too early from technical needs.

Wrong:

```text
JWT

Token

API

Express
```

These are implementation details, not business entities.

---

## Mistake 5

Adding fields immediately.

Don't write:

```text
User

↓

name

email

password
```

Fields come later.

Right now, only identify the business objects.

---

# Best Practices

- Read requirements carefully.
    
- Highlight nouns.
    
- Ignore verbs.
    
- Merge duplicate concepts.
    
- Separate entities from actions.
    
- Don't think about fields yet.
    
- Don't think about MongoDB or SQL yet.
    
- Focus only on the business objects.
    

---

# Module 3 Summary

By the end of this module, you should be able to:

- Identify entities from business requirements.
    
- Distinguish entities from actions and features.
    
- Merge similar concepts into a single entity.
    
- Recognize hidden relationship entities like **Like**, **Follow**, or **Enrollment**.
    
- Avoid premature schema design.
    
- Build a clean list of business objects before moving to relationships.
    

---

# Mini Exercise

Analyze the following **Food Delivery Application** requirements and identify the entities.

Requirements:

```text
Customers can register.
Restaurants can list food items.
Customers place orders.
Delivery partners deliver orders.
Customers can rate restaurants.
Customers can apply coupons.
Restaurants receive payments.
Admins manage users and restaurants.
```

Try to identify:

1. Core entities.
    
2. Relationship entities (if any).
    
3. Which nouns are **not** separate entities.
    
4. Which actions should **not** become entities.
    
5. Which entities may change state (for example, using a `status` field instead of creating multiple entities).
    

> **Next Module:** **Module 4 — Draw the ER Diagram**, where you'll connect these entities visually and begin modeling how they relate to each other before writing any database schema.