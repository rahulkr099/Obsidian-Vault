# Module 2 — Find the Queries

> **Goal:** Learn to identify the database queries your application will execute before designing tables or collections.

---

# Why This Module Matters

One of the biggest differences between beginners and experienced backend engineers is this:

**Beginners ask:**

> "What tables do I need?"

**Backend engineers ask:**

> "What data will the application need to retrieve, create, update, and delete?"

Your database exists to answer queries efficiently.

If you don't know the queries, you can't design a good schema or choose the right indexes.

---

# The Engineering Mindset

Think about the flow:

```text
Business Requirements
        ↓
User Stories
        ↓
Application Queries
        ↓
Entities
        ↓
Relationships
        ↓
Database Schema
```

Notice that **queries come before schema design**.

---

# What Is a Query?

A query is simply a request for data.

Examples:

```text
Show the latest blog posts.

Find Rahul's profile.

Load comments for this post.

Search blogs by title.

Show unread notifications.

Update a user's password.
```

Every page in your application usually executes one or more queries.

---

# Step 1 — List Every Screen or API

Before thinking about MongoDB or PostgreSQL, list all pages (or API endpoints).

Example: Blog Application

```text
Home Page

Login

Register

Profile

Create Post

Edit Post

Blog Details

Search

Dashboard

Admin Panel
```

Each screen needs data.

---

# Step 2 — Ask: "What Data Does This Screen Need?"

### Home Page

Needs:

```text
Latest published posts

Author name

Cover image

Published date

Number of likes
```

Possible query:

```sql
SELECT latest published posts
ORDER BY publishedAt DESC
LIMIT 10
```

---

### Profile Page

Needs:

```text
User information

User's published posts

Followers count

Following count
```

Possible queries:

```text
Find user by username

Find all posts by user

Count followers

Count following
```

---

### Blog Details Page

Needs:

```text
Post

Author

Comments

Likes

Related posts
```

Queries:

```text
Load post by slug

Load author

Load comments

Count likes

Find related posts
```

---

# Step 3 — Classify Queries

Every backend application has four main types of operations.

## 1. Create

Examples:

```text
Register user

Create post

Add comment

Like post
```

These insert new data.

---

## 2. Read

Examples:

```text
View profile

Read blog

Search posts

Load comments
```

These are the most common queries.

---

## 3. Update

Examples:

```text
Edit profile

Update password

Edit post

Publish draft
```

---

## 4. Delete

Examples:

```text
Delete comment

Delete post

Remove follower
```

Often implemented as **soft delete**.

---

# Step 4 — Identify Frequently Executed Queries

Some queries run much more often than others.

Example:

```text
Homepage

Runs thousands of times daily.
```

```text
Register user

Runs only a few times daily.
```

The homepage query deserves more optimization.

---

# Step 5 — Separate User Queries and Admin Queries

### User Queries

```text
View posts

Search posts

Comment

Like

Edit profile
```

---

### Admin Queries

```text
Delete inappropriate posts

Ban users

Approve reports

View analytics
```

Admin queries often require different permissions and indexes.

---

# Step 6 — Write Queries in Plain English

Avoid SQL or MongoDB syntax initially.

Good:

```text
Find all published posts.

Find comments for a post.

Find posts written by Rahul.

Search posts containing "Node.js".

Find users who follow Rahul.
```

Once the query is clear, implementation becomes easy.

---

# Step 7 — Identify Filters

Many queries filter data.

Examples:

```text
Status = Published

Author = Rahul

Category = Technology

Tag = MongoDB

Created after yesterday
```

These filters often become indexes later.

---

# Step 8 — Identify Sorting

Ask:

How should results be ordered?

Examples:

```text
Newest first

Oldest first

Most liked

Most viewed

Alphabetical
```

Example query:

```text
Latest published posts

↓

Sort by publishedAt DESC
```

Sorting heavily influences index design.

---

# Step 9 — Identify Pagination

Never load everything.

Wrong:

```text
Load all posts.
```

Correct:

```text
Load first 10 posts.

Load next 10 posts.

Load previous 10 posts.
```

Example:

```text
Page 1

10 posts

↓

Page 2

10 posts
```

Pagination is essential for scalable applications.

---

# Step 10 — Think About Search

Search is different from filtering.

Filtering:

```text
Category = Technology
```

Search:

```text
"Express"

"MongoDB"

"Authentication"
```

Search often requires text indexes or dedicated search engines.

---

# Step 11 — Think About Counts

Many pages display numbers.

Examples:

```text
Likes count

Comments count

Followers count

Views

Unread notifications
```

Ask:

Should these be calculated every time or stored?

Example:

```text
likesCount
```

Stored in the post document for faster reads.

---

# Step 12 — Think About Aggregations

Some queries summarize data.

Examples:

```text
Top authors

Most viewed posts

Monthly revenue

Daily signups

Average rating
```

Aggregation queries can become expensive, so identify them early.

---

# Step 13 — Think About Permissions

Not every query is available to everyone.

Example:

```text
User

↓

Can edit only their own posts.
```

```text
Admin

↓

Can edit any post.
```

Permissions affect how queries are written.

---

# Example Walkthrough — Blog Application

### Home

Queries:

```text
Load latest published posts.

Load trending posts.

Load featured authors.
```

---

### Blog Details

Queries:

```text
Find post by slug.

Find author.

Load comments.

Count likes.

Increment views.
```

---

### User Dashboard

Queries:

```text
Load drafts.

Load published posts.

Load archived posts.

Show analytics.
```

---

### Search

Queries:

```text
Search by title.

Search by author.

Search by tag.

Search by category.
```

---

### Admin Dashboard

Queries:

```text
Find reported posts.

Find inactive users.

Delete spam comments.

View system statistics.
```

---

# Example Walkthrough — E-commerce

Requirements:

```text
Users buy products.
```

Possible queries:

```text
Load product by ID.

Search products.

Filter by category.

Filter by price.

Sort by popularity.

View product reviews.

Add item to cart.

Checkout.

Track order.

Cancel order.

View order history.
```

Notice how we still haven't designed any tables.

---

# Common Beginner Mistakes

## Mistake 1

Designing tables before understanding queries.

Wrong:

```text
Product

Order

Cart
```

Correct:

```text
What operations will the application perform?
```

---

## Mistake 2

Ignoring read performance.

Most applications perform many more reads than writes.

Optimize for your most frequent queries.

---

## Mistake 3

Forgetting pagination.

Wrong:

```text
Load all users.
```

Correct:

```text
Load 20 users at a time.
```

---

## Mistake 4

Not considering sorting and filtering.

Always ask:

- Will users search?
    
- Will users filter?
    
- Will users sort?
    

---

## Mistake 5

Mixing business logic with query planning.

At this stage, only identify **what data is needed**, not how you'll code it.

---

# Real-World Example

Imagine you're building a **URL Shortener**.

Requirements:

```text
Users shorten URLs.

Users view analytics.

Users create custom aliases.

Users manage links.
```

Possible queries:

```text
Find URL by short code.

Create new short URL.

Load all links created by a user.

Count total clicks.

Show click history.

Show top-performing links.

Delete expired links.
```

Already, you can predict that:

- `shortCode` must be searched quickly.
    
- Analytics queries may need aggregation.
    
- User dashboard needs pagination.
    

These insights will guide your schema and indexes in later modules.

---

# Best Practices

- Write queries in plain English first.
    
- List queries for every screen and API.
    
- Separate create, read, update, and delete operations.
    
- Identify filters, sorting, pagination, and search needs.
    
- Highlight frequently executed queries.
    
- Think about permissions and aggregation early.
    

---

# Module 2 Summary

By the end of this module, you should be able to:

- Convert requirements into application queries.
    
- Identify the data needed for every screen or endpoint.
    
- Classify queries as Create, Read, Update, or Delete (CRUD).
    
- Recognize filters, sorting, pagination, and search requirements.
    
- Identify frequently executed and performance-critical queries.
    
- Plan for counts, aggregations, and permission-based access.
    

---

# Mini Exercise

Analyze the following **Learning Management System (LMS)** requirements and list the application queries.

Requirements:

```text
Students can enroll in courses.
Teachers can create courses.
Teachers can upload lessons.
Students can watch lessons.
Students can complete quizzes.
Students can view progress.
Teachers can see course analytics.
Admins can manage users.
```

Try to identify:

1. Queries for the Student Dashboard.
    
2. Queries for the Teacher Dashboard.
    
3. Queries for the Admin Panel.
    
4. Frequently executed queries.
    
5. Filters, sorting, and pagination needs.
    
6. Search queries.
    
7. Aggregation queries (analytics, counts, reports).
    

> **Next Module:** **Module 3 — Discover the Entities**, where you'll learn how to convert these queries into well-designed database entities (tables/collections) without jumping straight into field definitions.