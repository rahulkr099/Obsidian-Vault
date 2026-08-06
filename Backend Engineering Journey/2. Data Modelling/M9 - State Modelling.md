# Module 9 — State Modeling

> **Goal:** Learn how to represent the lifecycle of your business objects using **states** instead of multiple boolean flags, making your backend simpler, safer, and easier to extend.

---

# Why This Module Matters

Every real application has objects that **change over time**.

Examples:

- A blog post starts as a draft and later becomes published.
    
- An order starts as pending and later becomes delivered.
    
- A support ticket moves from open to closed.
    
- A payment starts as pending and becomes successful or failed.
    

Many beginners model these using lots of boolean fields.

Example:

```javascript
{
    isDraft: false,
    isPublished: true,
    isArchived: false,
    isDeleted: false
}
```

This looks simple...

Until someone accidentally saves:

```javascript
{
    isDraft: true,
    isPublished: true,
    isArchived: true
}
```

Now the post is in **three states at the same time.**

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
Schema Design
      ↓
State Modeling   ← You are here
      ↓
Validation
      ↓
Indexes
```

---

# What Is a State?

A **state** represents the current stage of an entity in its lifecycle.

Think of a traffic signal.

```text
Red
↓

Yellow
↓

Green
```

A traffic light cannot be:

```text
Red

AND

Green
```

at the same time.

Business objects work the same way.

---

# State vs Boolean Flags

## Bad Design

```javascript
{
    isPending: true,
    isApproved: false,
    isRejected: false
}
```

Later someone writes:

```javascript
{
    isPending: true,
    isApproved: true,
    isRejected: false
}
```

Impossible situation.

---

## Better Design

```javascript
{
    status: "pending"
}
```

Possible values:

```text
pending

approved

rejected
```

Only one value can exist.

---

# Why States Are Better

A single state:

- Prevents impossible combinations.
    
- Makes code easier to understand.
    
- Simplifies database queries.
    
- Makes future changes easier.
    

---

# Step 1 — Find Objects That Change

Ask:

> **Can this entity change over time?**

Examples:

```text
Blog Post
```

Yes.

---

```text
Order
```

Yes.

---

```text
Payment
```

Yes.

---

```text
Comment
```

Maybe.

---

```text
Category
```

Usually not.

---

# Step 2 — Identify All Possible States

Example:

Blog Post

Possible lifecycle:

```text
Draft

↓

Published

↓

Archived

↓

Deleted
```

These become your state values.

---

Example:

Order

```text
Pending

↓

Confirmed

↓

Packed

↓

Shipped

↓

Delivered
```

---

Example:

Payment

```text
Pending

↓

Successful

↓

Failed

↓

Refunded
```

---

# Step 3 — Draw the State Diagram

Professional engineers often sketch state transitions.

Example:

```text
Draft
   |
Publish
   |
Published
   |
Archive
   |
Archived
```

Notice:

A post does **not** jump directly from:

```text
Draft

↓

Archived
```

unless business rules allow it.

---

# Step 4 — Name States Clearly

Bad:

```text
1

2

3
```

Good:

```text
draft

published

archived

deleted
```

State values should explain themselves.

---

# Example 1 — Blog Application

Wrong:

```javascript
{
    isDraft: false,
    isPublished: true,
    isDeleted: false,
    isArchived: false
}
```

Correct:

```javascript
{
    status: "published"
}
```

Possible values:

```text
draft

published

archived

deleted
```

---

# Example 2 — Todo Application

Wrong:

```javascript
{
    isCompleted: false,
    isDeleted: false
}
```

Better:

```javascript
{
    status: "in_progress"
}
```

Possible states:

```text
todo

in_progress

completed

cancelled
```

Now the workflow is obvious.

---

# Example 3 — Food Delivery

Order lifecycle:

```text
Pending

↓

Accepted

↓

Preparing

↓

Out for Delivery

↓

Delivered
```

Database:

```javascript
{
    status: "preparing"
}
```

---

# Example 4 — E-commerce

Order:

```text
Pending

↓

Confirmed

↓

Packed

↓

Shipped

↓

Delivered

↓

Returned
```

Notice:

Returned is another valid state.

No need for:

```javascript
isReturned
```

---

# Example 5 — URL Shortener

Short URL:

Possible states:

```text
Active

Expired

Disabled
```

Instead of:

```javascript
{
    isExpired: false,
    isDisabled: false
}
```

Use:

```javascript
{
    status: "active"
}
```

---

# Step 5 — Define Valid Transitions

Not every transition should be allowed.

Example:

```text
Draft

↓

Published

↓

Archived
```

Allowed.

---

But:

```text
Archived

↓

Draft
```

Maybe not.

---

Example:

Order

Allowed:

```text
Pending

↓

Confirmed
```

Allowed:

```text
Confirmed

↓

Packed
```

Not allowed:

```text
Delivered

↓

Pending
```

Business rules control transitions.

---

# Step 6 — Enforce State Changes in the Service Layer

Example:

Wrong:

```javascript
order.status = "Delivered";
```

from anywhere.

Better:

```javascript
order.confirm();
order.ship();
order.deliver();
```

or

```javascript
changeOrderStatus(order, "shipped");
```

The service checks:

- Is this transition valid?
    
- Does the user have permission?
    
- Are prerequisites complete?
    

---

# Example State Machine

Blog Post

```text
Draft
  |
Publish
  |
Published
  |
Archive
  |
Archived
```

Possible actions:

```text
Draft

↓

Edit

↓

Draft
```

```text
Published

↓

Edit

↓

Published
```

State diagrams help visualize workflows.

---

# State Modeling in MongoDB

Example:

```javascript
{
    title: "Learning MongoDB",

    status: "draft"
}
```

Validation:

```text
Allowed Values

draft

published

archived

deleted
```

Mongoose Enum:

```javascript
status: {
    type: String,
    enum: [
        "draft",
        "published",
        "archived",
        "deleted"
    ]
}
```

This prevents invalid states.

---

# Real-World Examples

## User Account

States:

```text
Pending Verification

↓

Active

↓

Suspended

↓

Deleted
```

---

## Payment

States:

```text
Pending

↓

Processing

↓

Successful

↓

Failed

↓

Refunded
```

---

## Support Ticket

States:

```text
Open

↓

Assigned

↓

In Progress

↓

Resolved

↓

Closed
```

---

## Ride Sharing

Ride:

```text
Requested

↓

Driver Assigned

↓

Accepted

↓

Started

↓

Completed

↓

Cancelled
```

---

## LMS

Course:

```text
Draft

↓

Published

↓

Archived
```

---

Student Enrollment:

```text
Enrolled

↓

Completed

↓

Dropped
```

---

# State vs Lifecycle

A state is just one point.

Example:

```text
Pending
```

A lifecycle is the complete journey.

```text
Pending

↓

Approved

↓

Completed
```

Understanding the lifecycle helps you build better systems.

---

# Common Beginner Mistakes

## Mistake 1

Using many booleans.

Wrong:

```javascript
isApproved

isRejected

isPending
```

Correct:

```javascript
status
```

---

## Mistake 2

Using unclear state names.

Wrong:

```text
done

ok

finished
```

Better:

```text
completed
```

---

## Mistake 3

Allowing invalid transitions.

Example:

```text
Delivered

↓

Pending
```

Should not happen.

---

## Mistake 4

Not validating state values.

Use enums or constants.

---

## Mistake 5

Hardcoding strings everywhere.

Instead of:

```javascript
if(order.status === "delivered")
```

Prefer:

```javascript
ORDER_STATUS.DELIVERED
```

Example:

```javascript
const ORDER_STATUS = {
    PENDING: "pending",
    SHIPPED: "shipped",
    DELIVERED: "delivered"
};
```

This reduces typos and improves maintainability.

---

# Best Practices

- Use one `status` field instead of multiple boolean flags.
    
- Model the complete lifecycle of an entity.
    
- Define valid state transitions.
    
- Validate allowed state values.
    
- Keep state names descriptive and consistent.
    
- Centralize state constants.
    
- Handle state changes in the service layer, not directly in controllers.
    

---

# Real Backend Example

Suppose you're building an **Order Management System**.

Schema:

```javascript
{
    _id,
    customer,
    items,
    totalAmount,
    status,
    createdAt
}
```

Possible values:

```text
pending

confirmed

packed

shipped

delivered

cancelled
```

Service logic:

```text
Pending
   ↓
Confirmed
   ↓
Packed
   ↓
Shipped
   ↓
Delivered
```

The service layer ensures:

- Only valid transitions occur.
    
- Notifications are sent at the right time.
    
- Inventory is updated.
    
- Payments are handled correctly.
    

This is much cleaner than dozens of boolean fields.

---

# Module 9 Summary

By the end of this module, you should be able to:

- Explain why state modeling is better than multiple boolean fields.
    
- Identify entities that have a lifecycle.
    
- Design clear and meaningful state values.
    
- Draw simple state transition diagrams.
    
- Define valid and invalid state transitions.
    
- Validate state values using enums or constants.
    
- Implement state changes safely through the service layer.
    

---

# Mini Exercise

Design the state model for an **Online Job Portal**.

Entities:

```text
Job

Application

Interview

User
```

For each entity:

1. List all possible states.
    
2. Draw the lifecycle.
    
3. Identify valid transitions.
    
4. Identify invalid transitions.
    
5. Decide whether a single `status` field is enough.
    
6. Think about which transitions should require authorization (for example, only recruiters can move an application from `reviewing` to `shortlisted`).
    

> **Next Module:** **Module 10 — Validation Rules**, where you'll learn how to protect your application by validating data at multiple layers (client, API, service, and database) and designing robust validation rules that prevent invalid data from ever entering your system.