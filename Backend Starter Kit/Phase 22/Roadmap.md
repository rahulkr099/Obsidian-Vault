# Phase 22 — Security Testing 🔐

You’ve finished **Phase 21 — Backend Testing**, so now we move from:

> **“Does my backend work?”**

to:

> **“Can an attacker break my backend?”**

This phase follows the roadmap in your uploaded starter-pack material, where Phase 22 is dedicated to security testing and includes threat modeling, OWASP API risks, broken authentication/authorization, IDOR, mass assignment, injection, JWT attacks, cookie attacks, CORS/CSRF, sensitive-data exposure, and security tests.

Your original architecture roadmap also places security testing after the normal testing layer, which is exactly where we're going next.

---

# 🎯 Phase 22 Goal

By the end of this phase, you should be able to look at an API and think like both:

```text
Developer
   +
Security Tester
```

Instead of only testing:

```text
POST /api/v1/todos
      ↓
201 Created ✅
```

you'll also test:

```text
Can another user create a Todo for me?       ❌
Can User A read User B's Todo?               ❌
Can normal user become admin?                ❌
Can expired JWT access the API?               ❌
Can refresh token be reused?                 ❌
Can malicious input reach MongoDB?           ❌
Can login be brute-forced?                   ❌
Can sensitive information leak in errors?     ❌
```

---

# Phase 22 Lessons

## 22.1 — What Is Security Testing?

Understand:

- Functional testing
    
- Security testing
    
- Positive testing
    
- Negative testing
    
- Abuse-case testing
    
- Adversarial testing
    

Mental model:

```text
Normal tester:
"What should happen?"

Security tester:
"What happens if I do something
the developer didn't expect?"
```

---

## 22.2 — Threat Modeling

Before attacking an API, identify:

```text
Assets
 ↓
Users
 ↓
Trust boundaries
 ↓
Attack surfaces
 ↓
Threats
 ↓
Mitigations
```

We'll create a simple threat model for your MERN backend.

---

## 22.3 — OWASP API Security Risks

We'll learn the major API security problems relevant to your backend.

Especially:

```text
Broken Object Level Authorization
Broken Authentication
Broken Object Property Level Authorization
Unrestricted Resource Consumption
Broken Function Level Authorization
Unrestricted Access to Sensitive Business Flows
Server-Side Request Forgery
Security Misconfiguration
Improper Inventory Management
Unsafe Consumption of APIs
```

The goal isn't memorizing names.

The goal is recognizing the **pattern of attack**.

---

# 22.4 — Broken Authentication

We'll deliberately test:

```text
Invalid password
Missing password
Wrong email
Expired token
Malformed token
Missing token
Modified token
Invalid refresh token
Revoked refresh token
```

For example:

```http
GET /api/v1/users/me
Authorization: Bearer invalid-token
```

Expected:

```text
401 Unauthorized
```

Not:

```text
500 Internal Server Error
```

---

# 22.5 — Broken Authorization

Authentication answers:

> Who are you?

Authorization answers:

> What are you allowed to do?

We'll test:

```text
USER → user endpoint       ✅
USER → admin endpoint      ❌

ADMIN → admin endpoint     ✅
```

We'll also test authorization at the **resource level**.

---

# 22.6 — IDOR / BOLA

This is one of the most important lessons.

Suppose:

```text
User A
  ↓
Todo 101

User B
  ↓
Todo 202
```

User A sends:

```http
GET /api/v1/todos/202
```

A vulnerable backend might do:

```js
Todo.findById(todoId);
```

and accidentally return User B's Todo.

Secure architecture:

```js
Todo.findOne({
    _id: todoId,
    userId: req.user.id
});
```

Test:

```text
User A → Todo A    ✅
User A → Todo B    ❌
User B → Todo B    ✅
```

This connects directly to the ownership architecture we established earlier.

---

# 22.7 — Mass Assignment

Imagine your user API accepts:

```json
{
  "name": "Rahul",
  "email": "rahul@example.com",
  "role": "admin"
}
```

If your backend blindly updates everything:

```js
User.findByIdAndUpdate(id, req.body);
```

an attacker might promote themselves.

We'll learn:

```text
❌ Trust req.body

        ↓

✅ Explicitly allow fields
```

For example:

```js
{
    name,
    email
}
```

but not:

```text
role
passwordHash
refreshTokenHash
```

---

# 22.8 — Injection Testing

We'll test malicious input against:

```text
MongoDB
Query parameters
Search
Filtering
Sorting
Regex
JSON payloads
```

Example concept:

```text
Normal:
email = user@example.com

Malicious:
email = unexpected query object
```

We'll learn why sanitization alone isn't enough.

The architecture should use:

```text
Validation
+
Allow-listing
+
Safe queries
+
Sanitization
```

---

# 22.9 — Rate-Limit Testing

We'll test endpoints such as:

```text
/login
/signup
/refresh
/forgot-password
```

Questions:

```text
How many attempts are allowed?
What happens after the limit?
Does the limit reset?
Can an attacker bypass it?
```

Example:

```text
Attempt 1 → 401
Attempt 2 → 401
Attempt 3 → 401
...
Attempt N → 429 Too Many Requests
```

---

# 22.10 — JWT Security Testing

We'll attack the authentication system from multiple directions:

```text
Missing JWT
Malformed JWT
Expired JWT
Modified JWT
Wrong secret
Wrong algorithm
Missing claims
Invalid issuer
Invalid audience
```

We'll also understand why JWT verification must be strict.

Mental model:

```text
Receive token
     ↓
Verify signature
     ↓
Verify expiration
     ↓
Verify expected claims
     ↓
Authenticate user
```

---

# 22.11 — Refresh Token Attacks

We'll test:

```text
Refresh token theft
Refresh token reuse
Expired refresh token
Revoked refresh token
Rotated refresh token
Invalid refresh token
```

The important concept:

```text
Refresh token
      ↓
Hash stored in database
      ↓
Presented token compared
```

We'll also examine token rotation and reuse detection.

---

# 22.12 — Cookie Security Testing

We'll inspect authentication cookies for:

```text
HttpOnly
Secure
SameSite
Domain
Path
Expiration
```

We'll understand attacks involving:

```text
Cookie theft
Cross-site requests
Insecure transport
Improper cookie scope
```

---

# 22.13 — CSRF Testing

We'll learn:

> When authentication uses cookies, the browser can automatically attach those cookies to requests.

That's why state-changing endpoints need careful CSRF protection.

We'll test:

```text
POST
PUT
PATCH
DELETE
```

rather than focusing only on GET requests.

---

# 22.14 — CORS Security Testing

We'll test:

```text
Allowed origin
Unknown origin
Null origin
Multiple origins
Credentials
Preflight
OPTIONS
```

We'll specifically look for dangerous configurations such as accidentally allowing arbitrary origins with credentials.

---

# 22.15 — Sensitive Data Exposure

We'll inspect:

```text
API responses
Error messages
Logs
JWT payloads
Database documents
Headers
Debug output
```

Things that should **never accidentally appear**:

```text
passwordHash
refreshTokenHash
resetToken
database credentials
JWT secrets
internal stack traces
private user information
```

We'll learn to test for leaks rather than simply assume they don't exist.

---

# 22.16 — Security Testing Checklist

We'll build a reusable checklist covering:

```text
Authentication
Authorization
Ownership
Input validation
Injection
Rate limiting
JWT
Refresh tokens
Cookies
CORS
CSRF
Error handling
Sensitive data
Security headers
Logging
Dependencies
```

This eventually becomes part of your backend starter workflow.

---

# 22.17 — Build Automated Security Tests

Now we turn manual security checks into automated tests.

For example:

```js
describe("Todo ownership", () => {
    it("should reject access to another user's todo", async () => {
        // ...
    });
});
```

We'll build tests for:

```text
401
403
404
429
IDOR
RBAC
mass assignment
JWT
refresh tokens
validation
```

---

# 22.18 — Security Test Database

We'll learn how to isolate security tests from your normal development database.

Architecture:

```text
Test Runner
     ↓
Test Database
     ↓
Seed users
     ↓
Seed resources
     ↓
Run attack
     ↓
Assert result
     ↓
Cleanup
```

This is especially important for ownership and authorization tests.

---

# 22.19 — Build an Attack-Test Matrix

We'll create something like:

|Area|Attack|Expected|
|---|---|---|
|Auth|Invalid JWT|401|
|Auth|Expired JWT|401|
|Auth|Missing JWT|401|
|RBAC|User → admin route|403|
|Ownership|User A → User B resource|403/404|
|Validation|Invalid input|400|
|Rate limit|Too many requests|429|
|Mass assignment|`role=admin`|Ignored/rejected|
|Injection|Malicious query|Rejected|
|Refresh|Reused token|Rejected|
|Data exposure|Password hash response|Never exposed|

This becomes your **security regression suite**.

---

# 22.20 — Final Security Testing Project

We'll finish Phase 22 by attacking the backend we built throughout Phases 14–21.

The final flow:

```text
                    YOUR API
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
     Authentication Authorization  Input
          │            │            │
          ▼            ▼            ▼
       JWT tests    IDOR tests   Injection
          │            │            │
          └────────────┼────────────┘
                       ▼
                 Attack tests
                       │
                       ▼
                 Security suite
                       │
                       ▼
                 PASS / FAIL
```

---

# 🧠 The Most Important Mindset

For normal testing:

```text
"Does this feature work?"
```

For security testing:

```text
"What happens if I abuse this feature?"
```

For example, don't only test:

```text
User creates Todo → success
```

Test:

```text
User creates Todo → success
User creates Todo without JWT → rejected
User creates Todo with invalid JWT → rejected
User edits another user's Todo → rejected
User deletes another user's Todo → rejected
User sends unknown fields → rejected/ignored
User sends malicious input → safely handled
User sends thousands of requests → rate limited
```

That's the mindset I want you to develop.

---

# 🗺️ Phase 22 Roadmap

So our lesson sequence will be:

```text
22.1  What Is Security Testing?
22.2  Threat Modeling
22.3  OWASP API Security Risks
22.4  Broken Authentication
22.5  Broken Authorization
22.6  IDOR / BOLA
22.7  Mass Assignment
22.8  Injection Testing
22.9  Rate-Limit Testing
22.10 JWT Security Testing
22.11 Refresh Token Attacks
22.12 Cookie Security Testing
22.13 CSRF Testing
22.14 CORS Security Testing
22.15 Sensitive Data Exposure
22.16 Security Testing Checklist
22.17 Automated Security Tests
22.18 Security Test Database
22.19 Attack-Test Matrix
22.20 Final Security Testing Project
```

This gives us a clean progression:

```text
Phase 21
Testing fundamentals
       ↓
Phase 22
Security testing
       ↓
Phase 23
Docker & Production Architecture
       ↓
Phase 24
Production Hardening
       ↓
Phase 25
Build the complete starter from zero
```

**Next: `lesson 22.1` — What Is Security Testing?**