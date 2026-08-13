# Phase 0 — Planning & System Design

Great. **Do not write application code yet.** Phase 0 is where we decide _what we are building and how the pieces will communicate_.

For your AI LMS, I recommend keeping Phase 0 to **6 lessons**.

---

## Phase 0 Roadmap

|Lesson|Topic|Output|
|---|---|---|
|**0.1**|Requirements & Scope|What the LMS will do|
|**0.2**|User Roles & Features|Student / Instructor / Admin|
|**0.3**|System Architecture|Frontend → Backend → DB → AI|
|**0.4**|Database & ER Design|Tables + relationships|
|**0.5**|API Design|REST endpoints|
|**0.6**|Project Structure & Development Plan|Folder structure + implementation order|

---

# 0.1 — Requirements & Scope

Before creating:

```text
React
Express
Prisma
PostgreSQL
```

we need to define the **MVP**.

Our first version should answer:

> "What is the smallest version of this LMS that is genuinely useful?"

## 🎯 AI LMS MVP

### Student

A student should be able to:

```text
Register
Login
Browse courses
View course details
Enroll in a course
View modules and lessons
Track lesson progress
Take quizzes
View quiz results
View overall course progress
Ask AI questions
```

### Instructor

An instructor should be able to:

```text
Register/login
Create courses
Create modules
Create lessons
Upload learning resources
Create quizzes
View enrolled students
View course analytics
```

### Admin

Admin should be able to:

```text
Manage users
Manage courses
Manage categories
View platform statistics
```

---

# 🤖 AI MVP

Don't build 10 AI features.

Start with **three**.

### 1. AI Tutor

Student asks:

> What is middleware in Express?

AI answers.

But eventually the answer should be based on the **course material**.

---

### 2. AI Quiz Generator

Instructor provides lesson content:

```text
"Generate 5 MCQs from this lesson."
```

AI generates questions.

---

### 3. AI Summarizer

Student opens a lesson:

```text
Lesson
 ↓
Generate Summary
 ↓
Key concepts
 ↓
Important points
```

These three are enough to demonstrate meaningful AI integration.

---

# 📌 Functional Requirements

Now let's write our requirements in a more engineering-oriented way.

### Authentication

```text
FR-01  User can register
FR-02  User can login
FR-03  User can logout
FR-04  User can refresh session
FR-05  User can reset password
```

### Authorization

```text
FR-06  System supports Student role
FR-07  System supports Instructor role
FR-08  System supports Admin role
FR-09  Users can access only authorized resources
```

### Courses

```text
FR-10  Instructor can create courses
FR-11  Instructor can update own courses
FR-12  Instructor can publish courses
FR-13  Student can browse courses
FR-14  Student can enroll in courses
```

### Learning

```text
FR-15  Student can view lessons
FR-16  System tracks lesson progress
FR-17  System calculates course progress
FR-18  Student can take quizzes
FR-19  System calculates quiz scores
```

### AI

```text
FR-20  Student can ask AI questions
FR-21  Instructor can generate quizzes using AI
FR-22  Student can generate lesson summaries
```

---

# 🔐 Non-Functional Requirements

These are often ignored by students, but they're excellent for your project documentation and interviews.

### Security

```text
NFR-01
Passwords must be securely hashed.

NFR-02
Protected APIs must require authentication.

NFR-03
Role-based authorization must be enforced on the backend.

NFR-04
User input must be validated.

NFR-05
AI endpoints must have rate limiting.
```

### Performance

```text
NFR-06
API responses should be reasonably fast.

NFR-07
Large files must not block normal API requests.

NFR-08
Frequently requested data may be cached using Redis.
```

### Reliability

```text
NFR-09
Errors should have consistent API responses.

NFR-10
Background jobs should support retries.

NFR-11
Database operations should maintain data integrity.
```

---

# 🚫 What We Are NOT Building in MVP

This is important.

We don't want the project to become:

```text
AI LMS
+ Payments
+ Live classes
+ Chat
+ Video conferencing
+ Mobile app
+ Microservices
+ Kubernetes
+ Kafka
+ Elasticsearch
+ Social network
+ Marketplace
```

😂

You'll never finish it.

Instead:

```text
                 AI LMS MVP
                     │
       ┌─────────────┼─────────────┐
       │             │             │
     Auth          Courses       Learning
       │             │             │
      RBAC       Enrollment      Progress
                                  │
                                Quiz
                     │
                    AI
                     │
              ┌──────┼──────┐
              │      │      │
            Tutor  Quiz   Summary
```

That's already a **serious project**.

---

# 🧠 One Important Architecture Decision

For your project, I strongly recommend:

## Modular Monolith

Not microservices.

Your backend can look like:

```text
backend/
│
├── auth/
├── users/
├── courses/
├── modules/
├── lessons/
├── enrollments/
├── progress/
├── quizzes/
├── certificates/
├── ai/
├── notifications/
└── shared/
```

Everything runs as one backend application.

But internally, the modules are separated.

Later, if you want to demonstrate scalability, you can explain:

> "The system currently uses a modular monolith architecture. AI processing and resource processing can be extracted into independent services as the platform scales."

That's a much more mature answer than saying:

> "I used microservices because it's scalable."

---

# 🏁 Phase 0 Deliverables

By the end of Phase 0, we should have:

```text
docs/
│
├── requirements.md
├── user-roles.md
├── architecture.md
├── database-design.md
├── api-design.md
└── development-plan.md
```

And diagrams:

```text
System Architecture
        ↓
Use Case Diagram
        ↓
ER Diagram
        ↓
API Architecture
```

We don't need to create these files immediately. We'll design each one during the lessons.

---

# Your Learning Path

I recommend we now go sequentially:

### **Lesson 0.1**

**Requirements & Scope** ← we just established the initial scope.

### **Lesson 0.2**

We'll design **Student, Instructor and Admin** in detail, including exactly what each role can and cannot do.

### **Lesson 0.3**

We'll design the **complete system architecture**.

### **Lesson 0.4**

We'll design the **PostgreSQL database and ER diagram**.

### **Lesson 0.5**

We'll design the **REST API**.

### **Lesson 0.6**

We'll create the **actual monorepo/project structure and implementation roadmap**.

**Next: Lesson 0.2 — User Roles & Feature Matrix.**