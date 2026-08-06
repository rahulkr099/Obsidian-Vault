# Module 7 — Design Attributes (Fields)

> **Goal:** Learn how to design clean, scalable, and maintainable entity attributes (fields) based on business requirements—not by guessing.

---

# Why This Module Matters

After completing Module 6, you know:

- What entities exist.
    
- How they relate.
    
- How each entity is uniquely identified.
    

Now it's time to answer:

> **"What information should each entity store?"**

This is where beginners often make their biggest mistakes.

Many either:

- Add too many fields.
    
- Miss important fields.
    
- Store duplicate data.
    
- Store data that belongs somewhere else.
    

Professional backend engineers design fields **intentionally**.

---

# The Engineering Flow

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
Attributes (Fields)   ← You are here
        ↓
Validation
        ↓
Indexes
```

---

# What Is an Attribute?

An attribute is a piece of information about an entity.

Example:

Entity:

```text
User
```

Attributes:

```text
name

email

username

password

bio

avatar
```

Every entity has attributes.

---

# Step 1 — Start With Business Requirements

Never invent fields.

Example requirement:

```text
Users can register.
```

Ask:

What information is required?

Answer:

```text
Name

Email

Password
```

Nothing more.

---

Requirement:

```text
Users can upload profile pictures.
```

Now add:

```text
avatar
```

The requirement drives the field—not your imagination.

---

# Step 2 — Add Only the Minimum Required Fields

A common beginner mistake is creating huge schemas.

Wrong:

```text
User

name

email

password

fatherName

motherName

bloodGroup

favoriteMovie

hobby

country

city

state

village

zip

phone

gender

linkedin

twitter

facebook
```

Unless the business needs these, don't add them.

Correct:

```text
User

name

email

password
```

Grow the schema when requirements grow.

---

# Step 3 — Categorize Fields

A useful technique is to group fields.

### Identity Fields

```text
_id

username

email

slug
```

---

### Business Fields

```text
title

content

price

description
```

---

### Relationship Fields

```text
author

postId

categoryId
```

---

### Status Fields

```text
status
```

---

### Audit Fields

```text
createdAt

updatedAt
```

Grouping fields improves readability.

---

# Step 4 — Choose Appropriate Data Types

Think about the data.

Example:

```text
Age
```

Should be:

```text
Number
```

---

Example:

```text
Email
```

Should be:

```text
String
```

---

Example:

```text
Created Date
```

Should be:

```text
Date
```

---

Example:

```text
Is Verified
```

Instead of:

```text
"Yes"

"No"
```

Use:

```text
Boolean
```

Choosing the correct data type avoids many bugs.

---

# Step 5 — Distinguish Required vs Optional Fields

Ask:

Can this entity exist without this field?

Example:

```text
User

email
```

Required.

---

```text
bio
```

Optional.

---

```text
avatar
```

Optional.

---

Blog Post

```text
title
```

Required.

---

```text
coverImage
```

Optional.

---

Don't make everything required.

---

# Step 6 — Decide Default Values

Some fields should have sensible defaults.

Example:

```text
status

↓

draft
```

---

```text
views

↓

0
```

---

```text
likesCount

↓

0
```

---

```text
isVerified

↓

false
```

Defaults simplify application logic.

---

# Step 7 — Use Meaningful Names

Bad:

```text
n

x

a

d

temp
```

Good:

```text
firstName

lastName

publishedAt

createdBy

profilePicture
```

Names should explain themselves.

---

# Step 8 — Avoid Duplicate Data

Example:

Post:

```text
title

authorName

authorEmail

authorPhone
```

Bad.

The author already exists.

Better:

```text
author
```

Reference the User entity.

Avoid storing the same information in multiple places.

---

# Step 9 — Store Facts, Not Calculations

Wrong:

```text
age
```

Age changes every year.

Store:

```text
dateOfBirth
```

Calculate age when needed.

---

Wrong:

```text
yearsOfExperience
```

Store:

```text
careerStartDate
```

Calculate the years.

Store stable facts.

---

# Step 10 — Avoid Multiple Boolean Fields for State

Wrong:

```text
isDraft

isPublished

isDeleted

isArchived
```

Impossible combinations can occur.

Example:

```text
true

true

false

true
```

Better:

```text
status

↓

draft

published

archived

deleted
```

One field.

One truth.

---

# Example — User Entity

Business requirements:

```text
Users register.

Users edit profile.

Users upload avatar.
```

Fields:

```text
_id

name

username

email

password

avatar

bio

status

createdAt

updatedAt
```

Notice:

No unnecessary fields.

---

# Example — Blog Post

Requirements:

```text
Create post.

Edit post.

Publish post.

View post.
```

Fields:

```text
_id

title

slug

content

author

status

coverImage

publishedAt

views

likesCount

createdAt

updatedAt
```

---

Notice:

We store:

```text
views
```

Because it changes frequently.

---

We do not store:

```text
readingTime
```

Unless required.

---

# Example — Comment

Requirements:

```text
Users comment.

Users reply.
```

Fields:

```text
_id

post

author

parentComment

content

status

createdAt

updatedAt
```

Notice:

No duplicated author information.

---

# Example — E-commerce Product

Requirements:

```text
Products have prices.

Products belong to categories.

Products have stock.
```

Fields:

```text
_id

name

description

price

stock

category

sku

images

status

createdAt

updatedAt
```

---

# Example — URL Shortener

Requirements:

```text
Users shorten URLs.

Users create aliases.

Users view analytics.
```

Fields:

```text
_id

shortCode

originalURL

createdBy

clickCount

expiresAt

createdAt
```

Notice:

We don't store analytics here.

Those belong in a different entity like:

```text
ClickEvent
```

---

# Example — ClickEvent

Fields:

```text
_id

shortURL

timestamp

ipAddress

country

device

browser

referrer
```

Each click is its own record.

---

# Step 11 — Think About Future Growth

Ask:

Could this entity evolve?

Example:

Today:

```text
Product

price
```

Tomorrow:

```text
price

discountPrice

currency
```

Don't over-engineer, but leave room for reasonable growth.

---

# Step 12 — Review Every Field

Ask:

```text
Why does this field exist?
```

If you can't answer, remove it.

Every field should have a business purpose.

---

# Common Beginner Mistakes

## Mistake 1

Adding fields "just in case."

Wrong:

```text
middleName

favoriteColor

nickname
```

Unless required.

---

## Mistake 2

Duplicating information.

Wrong:

```text
Post

authorName

authorEmail
```

Use:

```text
author
```

---

## Mistake 3

Using unclear names.

Wrong:

```text
x

temp

value
```

Use descriptive names.

---

## Mistake 4

Storing calculated values unnecessarily.

Wrong:

```text
age
```

Better:

```text
dateOfBirth
```

---

## Mistake 5

Using multiple booleans for state.

Wrong:

```text
isDraft

isPublished

isDeleted
```

Use:

```text
status
```

---

# Best Practices

- Let requirements determine fields.
    
- Start with the minimum.
    
- Choose appropriate data types.
    
- Separate required and optional fields.
    
- Use defaults where appropriate.
    
- Store facts instead of calculations.
    
- Avoid duplication.
    
- Use descriptive names.
    
- Review every field before implementation.
    

---

# Real-World Attribute Design Checklist

For every field, ask:

```text
Why is this field needed?

Who uses it?

Is it required?

Can it change?

Should it have a default value?

Is it duplicated elsewhere?

Does it belong to another entity?

Is the data type correct?

Can it be calculated instead?
```

If a field passes these questions, it's likely a good addition.

---

# Module 7 Summary

By the end of this module, you should be able to:

- Design attributes from business requirements.
    
- Keep schemas minimal and focused.
    
- Choose appropriate data types.
    
- Separate required and optional fields.
    
- Assign sensible default values.
    
- Avoid duplication and unnecessary calculated fields.
    
- Use clear, descriptive naming conventions.
    
- Review fields critically before implementation.
    

---

# Mini Exercise

Design the attributes for a **Task Management Application**.

Entities:

```text
User

Project

Task

Comment
```

Requirements:

```text
Users create projects.
Projects contain tasks.
Tasks have priorities.
Tasks can be assigned to users.
Users can comment on tasks.
Tasks can be completed.
```

For each entity:

1. List the minimum required fields.
    
2. Identify optional fields.
    
3. Choose suitable data types.
    
4. Assign default values where appropriate.
    
5. Decide which fields reference other entities.
    
6. Identify any fields that should **not** be stored because they can be calculated.
    

> **Next Module:** **Module 8 — Normalize vs. Denormalize**, where you'll learn one of the most important backend design decisions: **when to embed data, when to reference it, and when to intentionally duplicate data for performance.**