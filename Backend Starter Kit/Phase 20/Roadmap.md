# Phase 20 — Email & Background Work

Yes, Rahul. Based on the roadmap we established and your starter pack, **Phase 20 is Email Architecture & Background Work**. Your starter already has a `mail/` area with pieces such as a mail sender and templates, so this phase will explain **why that architecture exists and how to build it from scratch**.

The goal is **not** just to learn how to send an email.

The real goal is to understand:

> **How should a production backend handle work that does not need to block the HTTP request?**

---

## Phase 20 roadmap

We'll cover **15 lessons**:

```text
20.1  Why Email Belongs Outside Controllers
20.2  SMTP Fundamentals
20.3  Email Service Architecture
20.4  Building mailSender
20.5  Email Templates
20.6  Rendering Templates
20.7  Verification Emails
20.8  Password Reset Emails
20.9  Welcome & Notification Emails
20.10 Handling Email Failures
20.11 Synchronous vs Asynchronous Email
20.12 Background Jobs
20.13 Queue Fundamentals
20.14 Retry, Delay & Failure Handling
20.15 Build the Complete Email Architecture
```

### The big picture

We'll eventually reach this:

```text
HTTP Request
     │
     ▼
 Controller
     │
     ▼
 Service
     │
     ├──────────────► Database
     │
     └──────────────► Email Job
                          │
                          ▼
                       Queue
                          │
                          ▼
                       Worker
                          │
                          ▼
                     mailSender
                          │
                          ▼
                         SMTP
                          │
                          ▼
                    Email Provider
```

And this distinction is extremely important:

```text
HTTP request
     │
     ▼
"User registered"
     │
     ▼
Save user
     │
     ▼
Return response quickly
     │
     └────────► Email can happen separately
```

Rather than making the user wait unnecessarily:

```text
Request
  ↓
Create user
  ↓
Connect email server
  ↓
Render template
  ↓
Send email
  ↓
Wait...
  ↓
Finally respond
```

---

# 20.1 — Why Email Belongs Outside Controllers

We'll begin here because this is an **architecture lesson**, not an email-package lesson.

A beginner might write:

```js
export const signup = async (req, res) => {
    const user = await createUser(req.body);

    await sendEmail(
        user.email,
        "Welcome!"
    );

    res.status(201).json({
        success: true
    });
};
```

It works.

But now the controller knows about:

- user creation
    
- email sending
    
- email content
    
- email provider
    
- email failures
    

That's too much responsibility.

Instead:

```text
Controller
    ↓
Auth Service
    ↓
Create User
    ↓
Queue Email
```

The controller only handles HTTP.

---

# 20.2 — SMTP Fundamentals

Before using a library such as Nodemailer, understand what happens underneath.

Basic flow:

```text
Your Node.js application
        │
        ▼
     SMTP
        │
        ▼
 Mail server
        │
        ▼
 Recipient's mail server
        │
        ▼
     Inbox
```

We'll learn:

```text
SMTP
Host
Port
Username
Password
TLS
SSL
Authentication
Sender
Recipient
```

You'll understand why environment variables might look like:

```env
SMTP_HOST=
SMTP_PORT=
SMTP_USER=
SMTP_PASSWORD=
MAIL_FROM=
```

rather than blindly copying them.

---

# 20.3 — Email Service Architecture

We'll design a clean boundary:

```text
services/
    email.service.js
```

Its responsibility:

> "The application wants to send an email."

It should not need to know how every controller works.

For example:

```js
await emailService.sendVerificationEmail(user);
```

rather than:

```js
await transporter.sendMail({
    ...
});
```

inside your authentication controller.

---

# 20.4 — Building `mailSender`

Now we'll go one level deeper.

Your starter's `mail/` architecture is the kind of separation we're aiming for.

Conceptually:

```text
mail/
├── mailSender.js
├── renderTemplate.js
└── templates/
```

The responsibility of `mailSender` is simple:

```text
Receive email information
        ↓
Talk to SMTP/provider
        ↓
Send email
```

It should not decide:

```text
Should this user receive a verification email?
```

That is business/application logic.

---

# 20.5 — Email Templates

We don't want this:

```js
const html = `
<html>
<body>
<h1>Hello ${user.name}</h1>
...
</body>
</html>
`;
```

inside a service.

Instead:

```text
mail/
└── templates/
    ├── verification.ejs
    ├── password-reset.ejs
    └── welcome.ejs
```

Then:

```text
Service
   ↓
Choose template
   ↓
Render template
   ↓
Send rendered HTML
```

This gives us a clean separation between:

```text
Business logic
```

and:

```text
Email presentation
```

---

# 20.6 — Rendering Templates

We'll learn how template rendering works:

```text
Template
   +
Data
   ↓
Renderer
   ↓
HTML
```

For example:

```text
Template:

Hello <%= name %>
```

Data:

```js
{
    name: "Rahul"
}
```

Result:

```html
Hello Rahul
```

We'll also discuss an important security point:

> **Never treat user-controlled HTML as trusted template code.**

---

# 20.7 — Verification Emails

Now we connect email to authentication.

Flow:

```text
POST /signup
      │
      ▼
Validate input
      │
      ▼
Create user
      │
      ▼
Generate verification token
      │
      ▼
Store required verification state
      │
      ▼
Queue verification email
      │
      ▼
Return response
```

Email:

```text
Welcome!

Please verify your email:

[Verify Email]
```

The verification link might conceptually be:

```text
https://frontend.example.com/verify-email?token=...
```

We'll carefully discuss what should and should not be placed in that token.

---

# 20.8 — Password Reset Emails

Password reset is another excellent example of why email architecture matters.

Flow:

```text
POST /forgot-password
        │
        ▼
Find account
        │
        ▼
Generate reset token
        │
        ▼
Store hashed token
        │
        ▼
Queue email
        │
        ▼
Return generic response
```

Important security principle:

Even if the email does not exist, don't casually reveal:

```text
"That email isn't registered."
```

Instead, use a response that doesn't reveal account existence.

Then:

```text
User clicks link
       ↓
Frontend
       ↓
POST /reset-password
       ↓
Backend verifies token
       ↓
Update password
       ↓
Invalidate reset state
```

---

# 20.9 — Welcome & Notification Emails

Email isn't only for authentication.

We'll design reusable events such as:

```text
USER_REGISTERED
EMAIL_VERIFICATION_REQUIRED
PASSWORD_RESET_REQUESTED
PASSWORD_CHANGED
TODO_CREATED
ACCOUNT_UPDATED
```

Instead of thinking:

> "I need to send an email here."

Think:

> **"Something happened in my application, and an email may be one reaction to that event."**

That's a much more scalable mindset.

---

# 20.10 — Handling Email Failures

This is where backend engineering becomes interesting.

Suppose:

```text
User signs up
     ↓
Database succeeds
     ↓
Email fails
```

What should happen?

Should signup fail?

Not always.

You have to decide whether email is:

```text
critical
```

or:

```text
non-critical
```

For example:

### Critical

A payment confirmation may need strong guarantees.

### Potentially non-critical

A welcome email can often be retried separately.

So we need to think about:

```text
Database operation
       +
Email operation
```

as two separate reliability concerns.

---

# 20.11 — Synchronous vs Asynchronous Email

This is one of the most important lessons in Phase 20.

### Synchronous

```text
Request
  ↓
Service
  ↓
Send email
  ↓
Wait
  ↓
Response
```

### Asynchronous

```text
Request
  ↓
Service
  ↓
Create job
  ↓
Response
       \
        \
         ▼
        Queue
          ↓
        Worker
          ↓
       Send email
```

Why asynchronous?

Because email can be:

- slow
    
- temporarily unavailable
    
- rate limited
    
- retriable
    
- external to your application
    

We don't want an external dependency unnecessarily slowing every API request.

---

# 20.12 — Background Jobs

Now we move beyond email.

A **background job** is simply:

> Work that your application asks another process to perform outside the main request.

Examples:

```text
Send email
Generate report
Resize image
Process uploaded file
Send notification
Generate invoice
Clean old records
Sync external API
```

Basic architecture:

```text
API Server
    │
    ▼
Create Job
    │
    ▼
Queue
    │
    ▼
Worker
    │
    ▼
Perform Work
```

This is a major step toward production backend architecture.

---

# 20.13 — Queue Fundamentals

We'll learn the basic concepts:

```text
Producer
Queue
Consumer / Worker
Job
Payload
Retry
Delay
Failure
Dead-letter handling
```

Example:

```text
Auth Service
    │
    │ createEmailJob()
    ▼
┌───────────────┐
│     Queue     │
└───────┬───────┘
        │
        ▼
     Worker
        │
        ▼
   Email Service
```

We'll then see why a queue is different from simply doing:

```js
setTimeout(() => {
   sendEmail();
}, 5000);
```

`setTimeout()` is **not** a reliable background job system.

---

# 20.14 — Retry, Delay & Failure Handling

External services fail.

So a production worker needs concepts like:

```text
Attempt 1
   ↓
Failed
   ↓
Wait
   ↓
Attempt 2
   ↓
Failed
   ↓
Wait longer
   ↓
Attempt 3
```

This is commonly called:

> **retry with backoff**

We'll also discuss:

```text
max attempts
job timeout
duplicate jobs
idempotency
dead-letter queues
permanent failures
temporary failures
```

These concepts are useful far beyond email.

---

# 20.15 — Build the Complete Email Architecture

Finally we'll combine everything.

Target architecture:

```text
backend/
│
├── mail/
│   ├── mailSender.js
│   ├── renderTemplate.js
│   └── templates/
│       ├── verification.ejs
│       ├── password-reset.ejs
│       └── welcome.ejs
│
├── services/
│   ├── auth.service.js
│   └── email.service.js
│
├── jobs/
│   └── email.worker.js
│
└── ...
```

And the complete flow:

```text
                    SIGNUP
                      │
                      ▼
                  Controller
                      │
                      ▼
                  Auth Service
                   /        \
                  /          \
                 ▼            ▼
             Repository    Email Job
                 │             │
                 ▼             ▼
              MongoDB        Queue
                               │
                               ▼
                             Worker
                               │
                               ▼
                         Email Service
                               │
                               ▼
                         renderTemplate
                               │
                               ▼
                           mailSender
                               │
                               ▼
                              SMTP
                               │
                               ▼
                            User
```

---

# What you should know by the end

You should be able to answer these questions without memorizing:

### Why shouldn't controllers send emails directly?

Because controllers should handle HTTP, while email is an application/infrastructure concern.

### Why use templates?

To separate email presentation from application logic.

### Why use a queue?

To move slow/retriable work away from the HTTP request.

### What is a worker?

A process that consumes jobs and performs the actual background work.

### What happens when email fails?

The system should have an intentional failure/retry strategy instead of accidentally failing the entire request.

### Is email the only background job?

No.

```text
Email
Reports
Notifications
Images
Webhooks
Data processing
Scheduled cleanup
```

can all use the same general architecture.

---

## Phase 20 mental model

Keep this one:

```text
        HTTP REQUEST
             │
             ▼
        CONTROLLER
             │
             ▼
         SERVICE
             │
       ┌─────┴─────┐
       │           │
       ▼           ▼
   DATABASE      JOB
                   │
                   ▼
                 QUEUE
                   │
                   ▼
                WORKER
                   │
                   ▼
            EXTERNAL SERVICE
```

The deeper lesson of Phase 20 is actually:

> **Your API server should not have to do every piece of work itself.**

That's the bridge from a simple Express backend to a **production-grade backend architecture**.

**Next lesson: `20.1 — Why Email Belongs Outside Controllers`.****