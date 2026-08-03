# Module 8 — Normalize vs. Denormalize

> **Goal:** Learn when to store data once (normalize), when to intentionally duplicate data (denormalize), and when to embed or reference documents—especially in MongoDB.

---

# Why This Module Matters

This is one of the biggest differences between:

- Someone who **knows MongoDB**
    
- Someone who **designs databases professionally**
    

Many beginners believe:

> **"MongoDB means everything should be embedded."**

This is incorrect.

Professional backend engineers ask:

> **"Which design best supports the application's queries, performance, and future growth?"**

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
Normalization / Denormalization ← You are here
        ↓
Validation
        ↓
Indexes
```

Notice something important:

**We make this decision after understanding the application.**

Never before.

---

# What is Normalization?

Normalization means:

> **Store each piece of information only once.**

Example:

Instead of:

```text
Post

title

authorName

authorEmail

authorAvatar
```

Store:

```text
Post

title

authorId
```

User collection:

```text
User

name

email

avatar
```

Now the author's information exists in only one place.

---

## Benefits of Normalization

✅ Less duplicate data

✅ Easier updates

✅ Better consistency

✅ Smaller documents

Example:

Rahul changes his profile picture.

Normalized:

```text
User.avatar
```

Only one document changes.

Every post automatically uses the latest avatar.

---

# What is Denormalization?

Denormalization means:

> **Intentionally storing duplicate data to improve performance.**

Example:

Instead of calculating likes every request:

```text
Like Collection

↓

count()
```

Store:

```text
Post

likesCount = 1523
```

Now the homepage loads much faster.

---

## Benefits of Denormalization

✅ Faster reads

✅ Fewer database queries

✅ Better user experience

Perfect for:

- Dashboards
    
- Homepages
    
- Analytics
    
- Counters
    

---

# MongoDB Gives You Two Main Choices

## Option 1 — Embed

Store the child inside the parent.

Example:

```javascript
Post

{
    title: "...",

    author: "...",

    tags: [
        "Node",
        "MongoDB"
    ]
}
```

Everything is together.

---

## Option 2 — Reference

Store only the relationship.

Example:

```javascript
Post

{
    title: "...",

    author: ObjectId(...)
}
```

User collection:

```javascript
{
    _id: ...,

    name: "Rahul"
}
```

Later:

```javascript
populate()
```

or aggregation joins the data.

---

# The Biggest Beginner Question

> **Should I embed or reference?**

Instead of memorizing rules, ask a series of questions.

---

# Question 1

## Can the child exist without the parent?

Example:

Comment

Can a comment exist without a post?

No.

But...

Can comments become thousands?

Yes.

Therefore:

Still use a separate collection.

Not embedding.

---

Example:

Address

Can an address exist without a user?

Usually no.

One user.

One address.

Embedding makes sense.

---

# Question 2

## Will this data grow indefinitely?

Example:

Comments

```text
10

100

10,000

500,000
```

Never embed.

Documents become huge.

---

Example:

User Preferences

```text
Theme

Language

Timezone
```

Only a few fields.

Embedding is perfect.

---

# Question 3

## Does the child change frequently?

Example:

User Profile

Changes occasionally.

Embedding is okay.

---

Example:

Likes

Thousands of updates every day.

Separate collection is better.

---

# Question 4

## Is this data reused elsewhere?

Example:

Category

One category is shared by:

```text
Post A

Post B

Post C

Post D
```

Don't embed.

Reference it.

---

Example:

Author

One author writes:

```text
200 posts
```

Don't duplicate the author's profile everywhere.

Reference.

---

# Question 5

## How often do you read this data together?

Suppose every request loads:

```text
User

↓

Preferences
```

Always together.

Embedding is a good choice.

---

Suppose every request loads:

```text
Post

↓

Comments
```

Maybe.

Maybe not.

Separate collection is usually better.

---

# Example 1 — User Profile

Requirements:

```text
User has:

Theme

Language

Timezone
```

Design:

```javascript
User

{
    name,

    email,

    preferences: {

        theme,

        language,

        timezone

    }
}
```

Embed.

Small.

Always loaded together.

---

# Example 2 — Blog Comments

Bad Design

```javascript
Post

{

comments:[

...

...

...

50000 comments

]
}
```

Problems:

- Huge document
    
- Slow updates
    
- Large network transfer
    
- MongoDB document size limit
    

Better:

```text
Post Collection

Comment Collection
```

Comment:

```javascript
{

postId,

authorId,

content

}
```

Reference.

---

# Example 3 — Likes

Option 1

Calculate every request:

```javascript
Like.count()
```

Slow.

---

Option 2

Store:

```javascript
Post

likesCount
```

Now homepage becomes fast.

This is denormalization.

---

# Example 4 — Tags

Few tags:

```javascript
tags:

[
"Node",

"Express",

"MongoDB"
]
```

Embedding is fine.

---

If tags are shared across thousands of posts:

```text
Tag Collection

↓

Reference
```

Depends on requirements.

---

# Example 5 — URL Shortener

Entities:

```text
ShortURL

ClickEvent
```

Bad:

```javascript
ShortURL

{

clicks:[

100000 events

]
}
```

Very large.

Correct:

```text
ShortURL

↓

ClickEvent Collection
```

Reference.

---

# Example 6 — Todo Application

Todo

```javascript
{

title,

completed,

priority
}
```

Checklist

```javascript
checklist:

[

task1,

task2,

task3

]
```

Few checklist items.

Embedding works well.

---

# Example 7 — E-commerce

Product

```text
Category
```

Reference.

Because:

Many products share one category.

---

Shopping Cart

```javascript
Cart

{

items:[

...

...

]

}
```

Embedding often works.

Cart items belong only to one cart.

Limited size.

---

# Example 8 — LMS

Course

```text
Lessons
```

If:

```text
5 lessons
```

Embedding could work.

If:

```text
300 lessons

videos

quizzes

resources
```

Separate Lesson collection is better.

---

# Normalization vs Denormalization

|Question|Normalize|Denormalize|
|---|---|---|
|Duplicate data?|No|Yes|
|Read speed|Moderate|Faster|
|Write speed|Easier|Slightly more complex|
|Consistency|Excellent|Needs synchronization|
|Storage|Smaller|Larger|
|Typical use|Relationships|Counters, summaries, dashboards|

---

# Embed vs Reference

|Situation|Embed|Reference|
|---|---|---|
|Small data|✅||
|Always loaded together|✅||
|Doesn't grow much|✅||
|Shared by many entities||✅|
|Large collection||✅|
|Frequently updated||✅|
|Independent lifecycle||✅|

---

# Hybrid Design (Most Common)

Professional systems often combine both.

Example:

Post

```javascript
{

title,

authorId,

likesCount,

commentCount,

tags:[

"Node",

"Express"

]

}
```

Author:

Referenced.

Tags:

Embedded.

Counters:

Denormalized.

Comments:

Separate collection.

This is common in production.

---

# Real Blog Example

### User

```text
Reference
```

Reason:

One user owns many posts.

---

### Category

```text
Reference
```

Shared.

---

### Tags

```text
Embed

or

Reference

Depends on requirements.
```

---

### Comments

```text
Reference
```

Unlimited growth.

---

### Likes

```text
Reference

+

likesCount inside Post
```

Hybrid.

---

### Views

```text
views
```

Stored directly.

Denormalized.

---

# Common Beginner Mistakes

## Mistake 1

Embedding everything.

```javascript
User

Posts

Comments

Likes

Followers

Following
```

One giant document.

Very bad.

---

## Mistake 2

Referencing everything.

Even:

```text
Theme

Language

Timezone
```

This creates unnecessary joins.

---

## Mistake 3

Ignoring query patterns.

Always ask:

> What does the application read most often?

---

## Mistake 4

Calculating expensive values repeatedly.

Instead of:

```javascript
Like.count()
```

Store:

```javascript
likesCount
```

---

## Mistake 5

Not considering future growth.

Today:

```text
20 comments
```

Tomorrow:

```text
2 million comments
```

Design for realistic growth.

---

# Engineering Decision Framework

Whenever you are unsure, ask:

```text
1. Does it grow indefinitely?

2. Is it shared?

3. Is it always read together?

4. Does it change frequently?

5. Can it exist independently?

6. How often is it queried?

7. Is duplicate data acceptable?

8. Will this improve performance?
```

Answer these before choosing.

---

# Best Practices

- Normalize by default.
    
- Denormalize only when there is a clear performance benefit.
    
- Embed small, tightly related data.
    
- Reference large or shared data.
    
- Store counters instead of recalculating them repeatedly.
    
- Let application queries drive the design.
    
- Revisit your decisions as the application grows.
    

---

# Module 8 Summary

By the end of this module, you should be able to:

- Explain normalization and denormalization.
    
- Decide when to embed and when to reference data in MongoDB.
    
- Recognize situations where denormalized counters improve performance.
    
- Avoid oversized documents and unnecessary duplication.
    
- Use a hybrid approach that balances simplicity, consistency, and performance.
    

---

# Mini Exercise

Design the data model for a **Social Media Application**.

Entities:

```text
User

Post

Comment

Like

Follow

Notification
```

For each relationship, decide:

1. Embed or reference?
    
2. Normalize or denormalize?
    
3. Which counters should be stored?
    
4. Which data should always be loaded together?
    
5. Which collections could grow indefinitely?
    
6. Which information is shared across many entities?
    

> **Next Module:** **Module 9 — State Modeling**, where you'll learn how to model business workflows using states instead of multiple boolean flags, making your applications cleaner, safer, and easier to maintain.