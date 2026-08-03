# Module 10 — Validation Rules

> **Goal:** Learn how professional backend engineers validate data at every layer of the application to ensure only correct, secure, and consistent data enters the system.

---

# Why This Module Matters

Many beginners think validation means:

```javascript
if (!email) {
    return "Email is required";
}
```

Professional backend engineers think much bigger.

Validation is about protecting your system from:

- Invalid input
    
- Malicious input
    
- Broken business rules
    
- Data inconsistency
    
- Security vulnerabilities
    

A good backend **never trusts client data**.

> **Golden Rule:** **Validate everything that comes from outside your backend.**

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
Validation Rules   ← You are here
      ↓
Database Constraints
      ↓
Indexes
```

---

# What Is Validation?

Validation answers one simple question:

> **"Is this data acceptable?"**

Example:

User registers.

Request:

```json
{
    "name": "Rahul",
    "email": "rahul@gmail.com",
    "password": "Password123"
}
```

Before saving it, the backend checks:

- Is the name present?
    
- Is the email valid?
    
- Is the password strong enough?
    

Only then is it saved.

---

# Validation vs Business Rules

These are different.

## Validation

Checks if the **data format** is correct.

Example:

```text
Email is required.
```

```text
Password must be at least 8 characters.
```

```text
Age must be a number.
```

---

## Business Rule

Checks whether the **operation is allowed**.

Example:

```text
Only admins can delete users.
```

```text
A user can like a post only once.
```

```text
Orders cannot be cancelled after shipping.
```

Validation ensures correct input.

Business rules ensure correct behavior.

---

# The Four Layers of Validation

Professional applications validate data at multiple layers.

```text
Frontend
      ↓
API Validation
      ↓
Service Validation
      ↓
Database Validation
```

Never rely on just one layer.

---

# Layer 1 — Frontend Validation

Purpose:

Improve user experience.

Example:

```text
Email is empty.
```

Show error immediately.

Example:

```text
Password is too short.
```

User doesn't need to wait for the server.

But remember:

> Frontend validation can be bypassed.

Never trust it.

---

# Layer 2 — API Validation

This is your first line of defense in the backend.

Every incoming request should be validated.

Example:

```http
POST /users/register
```

Body:

```json
{
    "name": "Rahul",
    "email": "rahul@gmail.com",
    "password": "12345678"
}
```

Validate:

- Required fields
    
- Data types
    
- Length
    
- Format
    

If invalid:

```http
400 Bad Request
```

---

# Layer 3 — Service Validation

The service layer validates business logic.

Example:

Register user.

API validation already confirmed:

```text
Valid email.
```

Service validation checks:

```text
Does this email already exist?
```

Example:

User wants to publish a post.

Service checks:

```text
Does the user own this post?
```

Not a format issue.

A business rule.

---

# Layer 4 — Database Validation

The database should protect itself.

Examples:

```text
Email must be unique.
```

```text
Username must be unique.
```

```text
Status must be one of:

draft

published

archived
```

Even if your backend has a bug,

the database still prevents invalid data.

---

# Types of Validation

## 1. Required Validation

Example:

```json
{
    "title": ""
}
```

Invalid.

Rule:

```text
Title is required.
```

---

## 2. Data Type Validation

Wrong:

```json
{
    "age": "twenty"
}
```

Correct:

```json
{
    "age": 20
}
```

---

## 3. Length Validation

Username:

```text
Minimum:

3
```

Maximum:

```text
20
```

Password:

```text
Minimum:

8
```

---

## 4. Range Validation

Age:

```text
18–100
```

Price:

```text
Greater than zero
```

Rating:

```text
1–5
```

---

## 5. Format Validation

Email:

```text
rahul@gmail.com
```

Phone:

```text
9876543210
```

URL:

```text
https://example.com
```

Slug:

```text
mongodb-guide
```

---

## 6. Enum Validation

Only specific values are allowed.

Example:

```text
status
```

Allowed:

```text
draft

published

archived

deleted
```

Anything else:

```text
publish_now
```

Invalid.

---

## 7. Unique Validation

Example:

```text
Email
```

Only one user can own it.

Another example:

```text
Username
```

Should be unique.

---

## 8. Relationship Validation

User creates comment.

Check:

```text
Does this post exist?
```

User creates lesson.

Check:

```text
Does this course exist?
```

Relationships should be validated.

---

## 9. Ownership Validation

Example:

```text
Edit Post
```

Check:

```text
Does Rahul own this post?
```

Otherwise:

```http
403 Forbidden
```

---

## 10. State Validation

Example:

Order:

```text
Delivered
```

User requests:

```text
Cancel Order
```

Reject.

The current state doesn't allow it.

---

# Example — User Registration

Requirements:

```text
Name

Email

Password
```

Validation:

```text
Name required

2–50 characters
```

```text
Email required

Valid email format

Unique
```

```text
Password required

Minimum 8 characters

Maximum 100 characters
```

---

# Example — Blog Post

Fields:

```text
Title

Content

Status
```

Validation:

```text
Title required

Maximum 200 characters
```

```text
Content required
```

```text
Status

↓

draft

published

archived
```

---

# Example — URL Shortener

Fields:

```text
originalURL

shortCode
```

Validation:

```text
originalURL

↓

Valid URL
```

```text
shortCode

↓

Letters

Numbers

Length

Unique
```

---

# Example — E-commerce

Product:

```text
Price
```

Validation:

```text
Greater than zero
```

Stock:

```text
Greater than or equal to zero
```

Discount:

```text
0–100
```

Rating:

```text
1–5
```

---

# Validation Flow

Example:

```http
POST /posts
```

Flow:

```text
Receive Request
       ↓
Validate Request Body
       ↓
Validate Business Rules
       ↓
Validate Relationships
       ↓
Save to Database
```

If any step fails,

stop immediately.

---

# Validation Libraries

## Express + Joi

Example:

```javascript
const schema = Joi.object({
    email: Joi.string().email().required(),
    password: Joi.string().min(8).required()
});
```

---

## Zod

Popular in modern TypeScript projects.

Example:

```javascript
const schema = z.object({
    email: z.string().email(),
    password: z.string().min(8)
});
```

---

## Mongoose Validation

Example:

```javascript
email: {
    type: String,
    required: true,
    unique: true
}
```

Remember:

Mongoose validation is **not enough**.

Always validate before reaching the database.

---

# Error Messages

Bad:

```text
Invalid Input
```

Good:

```text
Email is required.
```

Better:

```text
Password must contain at least 8 characters.
```

Specific messages help users fix their mistakes.

---

# Common Beginner Mistakes

## Mistake 1

Trusting frontend validation.

Never do this.

Attackers can send requests directly to your API.

---

## Mistake 2

Only validating required fields.

Also validate:

- Length
    
- Format
    
- Range
    
- State
    
- Ownership
    
- Relationships
    

---

## Mistake 3

Putting all validation in controllers.

A cleaner architecture is:

```text
Controller

↓

Validation Middleware

↓

Service

↓

Repository
```

Controllers stay thin.

---

## Mistake 4

Using database validation as the only validation.

Bad.

Users receive poor error messages.

Validate before hitting the database.

---

## Mistake 5

Returning inconsistent errors.

Bad:

```json
{
    "message": "Invalid"
}
```

Better:

```json
{
    "success": false,
    "message": "Validation failed",
    "errors": [
        {
            "field": "email",
            "message": "Email is required"
        }
    ]
}
```

A consistent error format makes frontend integration much easier.

---

# Best Practices

- Validate every request entering your backend.
    
- Keep validation rules close to your API layer.
    
- Enforce business rules in the service layer.
    
- Use database constraints as the final safety net.
    
- Return clear and consistent error messages.
    
- Never trust client-side validation alone.
    
- Reuse validation schemas where possible.
    
- Validate relationships, ownership, and state—not just data formats.
    

---

# Validation Checklist

For every API endpoint, ask:

```text
Are all required fields present?

Are data types correct?

Are values within valid ranges?

Are formats correct?

Are enum values allowed?

Does every referenced entity exist?

Does the user own this resource?

Is the current state valid?

Will the database accept this data?
```

If all answers are **yes**, your request is ready to be processed.

---

# Module 10 Summary

By the end of this module, you should be able to:

- Explain the purpose of validation.
    
- Distinguish validation from business rules.
    
- Validate data at the frontend, API, service, and database layers.
    
- Apply different validation types (required, format, range, enum, relationship, ownership, and state).
    
- Design clear and consistent validation error responses.
    
- Integrate validation cleanly into a layered backend architecture.
    

---

# Mini Exercise

Design the validation rules for an **Event Booking System**.

Entities:

```text
User

Event

Booking

Ticket
```

Requirements:

```text
Users can create events.
Users can book tickets.
Events have limited seats.
Users cannot book the same event twice.
Bookings cannot be cancelled after the event starts.
Only organizers can edit their own events.
```

For each API (create event, update event, book ticket, cancel booking):

1. List the request validation rules.
    
2. List the business rule validations.
    
3. List the relationship validations.
    
4. List the ownership validations.
    
5. List the state validations.
    
6. Identify which validations belong in the API layer, service layer, and database.
    

> **Next Module:** **Module 11 — Database Constraints**, where you'll learn how to use the database itself to enforce data integrity with unique constraints, foreign keys (SQL), compound unique indexes, check constraints, and why application validation alone is never enough.