# Module 16 — Security Review

> **Goal:** Learn how to review your database schema and backend design from a security perspective so that sensitive data stays protected and users only access what they are authorized to see.

---

# Why This Module Matters

Many backend developers think security means:

- JWT
    
- HTTPS
    
- Password hashing
    

Those are important.

But security **starts much earlier**—during data modeling.

A poorly designed schema can expose sensitive information even if your authentication is perfect.

Imagine your API returns:

```json
{
    "_id": "...",
    "name": "Rahul",
    "email": "rahul@example.com",
    "password": "$2b$10$...",
    "refreshToken": "...",
    "resetToken": "...",
    "verificationToken": "..."
}
```

Even though the password is hashed, exposing these fields is a serious security mistake.

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
Schema Design
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
Audit Fields
      ↓
Security Review   ← You are here
      ↓
API Mapping
```

Before writing APIs, review your entire design for security.

---

# Security Mindset

Ask yourself:

> **"If an attacker calls this API, what information could they see or modify?"**

Don't assume users will behave correctly.

Assume they will try:

- Accessing other users' data
    
- Modifying hidden fields
    
- Guessing IDs
    
- Sending invalid requests
    
- Bypassing the frontend
    

Your backend must protect against all of these.

---

# Principle of Least Privilege

One of the most important security principles.

> **Every user should have access to only the data they actually need.**

Example:

A normal user should see:

```json
{
    "name": "Rahul",
    "avatar": "...",
    "bio": "Backend Developer"
}
```

They should **not** see:

```json
{
    "password": "...",
    "refreshToken": "...",
    "isAdmin": true
}
```

---

# Step 1 — Identify Sensitive Fields

Go through every entity.

Ask:

> "Should this field ever be sent to the client?"

---

## User Entity

Example:

```text
_id

name

username

email

password

refreshToken

resetToken

verificationToken

phone

role
```

Sensitive fields:

```text
password

refreshToken

resetToken

verificationToken
```

Usually hidden:

```text
role

phone
```

Depending on the API.

---

# Step 2 — Classify Data

A useful habit is to classify fields.

---

## Public Data

Safe for everyone.

Example:

```text
username

avatar

bio
```

---

## Private Data

Only the owner can access.

Example:

```text
email

phone

address
```

---

## Secret Data

Never expose.

Example:

```text
password

refreshToken

API keys

verification tokens
```

---

# Example Classification

|Field|Visibility|
|---|---|
|username|Public|
|avatar|Public|
|bio|Public|
|email|Owner/Admin|
|password|Never|
|refreshToken|Never|
|resetToken|Never|

This simple exercise prevents many data leaks.

---

# Step 3 — Never Store Plain Text Passwords

Wrong:

```json
{
    "password": "rahul123"
}
```

Correct:

```json
{
    "password": "$2b$10$..."
}
```

Passwords should always be hashed before storing.

Never encrypt passwords.

Hash them.

---

# Step 4 — Hide Sensitive Fields by Default

In Mongoose:

```javascript
password: {
    type: String,
    select: false
}
```

Now:

```javascript
User.find()
```

doesn't return the password unless explicitly requested.

This is an excellent safety measure.

---

# Step 5 — Review Every API Response

Example:

```http
GET /users/me
```

Should return:

```json
{
    "name": "Rahul",
    "email": "rahul@example.com",
    "avatar": "..."
}
```

Should NOT return:

```json
{
    "password": "...",
    "refreshToken": "...",
    "verificationToken": "..."
}
```

Always review your response objects.

---

# Step 6 — Protect Internal Fields

Some fields are meant only for the backend.

Example:

```text
internalNotes

fraudScore

adminComment

paymentGatewayResponse
```

These should never be exposed through public APIs.

---

# Step 7 — Ownership Checks

Authentication answers:

> Who are you?

Authorization answers:

> Are you allowed to do this?

Example:

Rahul tries:

```http
PUT /posts/123
```

Backend checks:

```text
Does post.authorId == Rahul's userId?
```

If not:

```http
403 Forbidden
```

This check belongs in the service layer.

---

# Step 8 — Role-Based Access Control (RBAC)

Instead of:

```javascript
isAdmin: true
```

Prefer:

```javascript
role: "admin"
```

Possible roles:

```text
user

admin

moderator

teacher

student
```

Now your application can grow without adding dozens of boolean flags.

---

# Example

Admin:

```text
Can delete posts.
```

Moderator:

```text
Can hide comments.
```

User:

```text
Can edit only their own profile.
```

The role determines permissions.

---

# Step 9 — Prevent Mass Assignment

Suppose your User schema contains:

```text
name

email

role

isVerified
```

User sends:

```json
{
    "name": "Rahul",
    "role": "admin"
}
```

If your backend blindly saves every field,

the attacker becomes an admin.

Instead, explicitly allow only safe fields.

Example:

```javascript
allowedFields = [
    "name",
    "avatar",
    "bio"
]
```

Ignore everything else.

---

# Step 10 — Protect Against ID Enumeration

Suppose:

```http
GET /orders/123
```

Attacker tries:

```http
GET /orders/124
```

```http
GET /orders/125
```

```http
GET /orders/126
```

Backend must verify ownership.

Never assume:

> "If they know the ID, they should see the data."

---

# Example — Blog Application

User entity:

Sensitive:

```text
password

refreshToken

resetToken
```

Hidden.

---

Post:

Only author can edit.

Everyone can read published posts.

Only admin can permanently delete.

---

Comment:

Only author or moderator can remove.

---

# Example — URL Shortener

Short URL:

Public:

```text
shortCode
```

Private:

```text
analytics

ownerId
```

Only owner should access analytics.

---

# Example — E-commerce

Order:

Customer can view:

```text
Their own order.
```

Cannot view:

```text
Other customers' orders.
```

Admin:

Can view all.

---

Product:

Everyone can view.

Only admins can edit.

---

# Example — Learning Management System

Teacher:

Can edit:

```text
Own courses.
```

Cannot edit:

```text
Other teachers' courses.
```

Student:

Can view:

```text
Published lessons.
```

Cannot modify:

```text
Grades.
```

---

# Security Review Checklist

Go through every entity.

Ask:

```text
Does this entity contain secrets?

Which fields should never leave the server?

Who owns this data?

Who can read it?

Who can update it?

Who can delete it?

Can users modify fields they shouldn't?

Can attackers guess another user's data?
```

If you can't answer these questions,

the design needs improvement.

---

# Data Exposure Matrix

Example:

|Field|Public|Owner|Admin|Never|
|---|:-:|:-:|:-:|:-:|
|username|✅|✅|✅||
|avatar|✅|✅|✅||
|bio|✅|✅|✅||
|email||✅|✅||
|phone||✅|✅||
|role|||✅||
|password||||✅|
|refreshToken||||✅|

Creating this table during design is an excellent habit.

---

# Common Beginner Mistakes

## Mistake 1

Returning the entire database document.

Wrong:

```javascript
res.json(user);
```

Instead:

Return only the required fields.

---

## Mistake 2

Storing passwords in plain text.

Always hash passwords.

---

## Mistake 3

Trusting client input.

Never allow clients to set:

```text
role

isVerified

createdBy

deletedBy
```

These are backend-controlled fields.

---

## Mistake 4

Skipping ownership checks.

Just because a user is logged in doesn't mean they own the resource.

---

## Mistake 5

Using booleans for permissions.

Instead of:

```javascript
isAdmin
isTeacher
isModerator
```

Use:

```javascript
role
```

or, for larger systems, a permission-based model.

---

# Best Practices

- Classify fields as public, private, or secret.
    
- Hash passwords before storing them.
    
- Hide sensitive fields by default.
    
- Never return entire database documents.
    
- Enforce ownership checks in the service layer.
    
- Use role-based authorization instead of multiple boolean flags.
    
- Prevent mass assignment by allowing only specific fields to be updated.
    
- Review every API response for accidental data exposure.
    

---

# Security Review Example

Imagine you're building a **Banking Application**.

Entity:

```text
Account
```

Fields:

```text
accountNumber

balance

PIN

owner

createdAt
```

Review:

|Field|Visibility|
|---|---|
|accountNumber|Owner/Admin|
|balance|Owner/Admin|
|PIN|Never|
|owner|Backend Only|
|createdAt|Admin/Internal|

The schema now reflects security requirements before any code is written.

---

# Module 16 Summary

By the end of this module, you should be able to:

- Review schemas from a security perspective.
    
- Classify fields by visibility.
    
- Protect sensitive information from being exposed.
    
- Understand ownership and authorization checks.
    
- Prevent mass assignment vulnerabilities.
    
- Design role-based access control.
    
- Apply the principle of least privilege to your backend APIs.
    

---

# Mini Exercise

Perform a security review for a **Hospital Management System**.

Entities:

```text
Patient

Doctor

Appointment

MedicalRecord

Prescription

Invoice
```

For each entity:

1. Identify public, private, and secret fields.
    
2. Decide who can read each field (patient, doctor, admin).
    
3. Decide who can update each field.
    
4. Identify fields that should never be exposed in API responses.
    
5. List ownership checks that should be enforced.
    
6. Identify backend-controlled fields that users should never be allowed to modify.
    

> **Next Module:** **Module 17 — API Mapping**, where you'll connect everything you've learned—requirements, queries, entities, relationships, validation, security, and indexes—to well-designed REST APIs that naturally fit your data model and business workflows.