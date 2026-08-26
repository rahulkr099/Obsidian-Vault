# Phase 21 — Backend Testing Architecture

Yes, Rahul. **Phase 21 is Testing Backend Architecture.**

This is the natural next step after:

```text
Phase 17 → CRUD Architecture
Phase 18 → Pagination / Filtering / Sorting
Phase 19 → Logging & Observability
Phase 20 → Email Architecture
Phase 21 → Testing Backend Architecture
```

This phase is important because we won't just learn **Jest syntax**. We'll learn how to test the architecture you've been building:

```text
Request
   ↓
Route
   ↓
Middleware
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
Model
   ↓
MongoDB
```

The goal is to know **which layer should be tested, what should be mocked, and when you should test the complete request.**

Your uploaded starter-pack roadmap also places testing after the application architecture and before security testing, Docker, and production hardening.

---

# Phase 21 Roadmap

We'll do **19 lessons**:

```text
21.1  Why Backend Testing Matters
21.2  Testing Pyramid
21.3  Jest Fundamentals
21.4  Test Structure & Assertions
21.5  Unit Testing Utilities
21.6  Testing Middleware
21.7  Testing Validation
21.8  Testing Services
21.9  Mocking Dependencies
21.10 Testing Repositories
21.11 Testing Controllers
21.12 Integration Testing
21.13 Supertest
21.14 Testing Authentication
21.15 Testing Authorization
21.16 Testing CRUD APIs
21.17 Test Database & Isolation
21.18 Fixtures, Factories & Coverage
21.19 Build the Complete Backend Test Architecture
```

---

# What you'll understand by the end

You'll be able to distinguish:

### Unit test

```text
service
   ↓
mock repository
```

### Integration test

```text
service
   ↓
repository
   ↓
test database
```

### API/E2E-style test

```text
HTTP request
   ↓
Express
   ↓
middleware
   ↓
controller
   ↓
service
   ↓
repository
   ↓
database
```

And you'll understand **why we don't use one type of test for everything.**

---

# The final testing architecture

By the end, your backend should have something conceptually like:

```text
tests/
│
├── unit/
│   ├── utils/
│   ├── middleware/
│   ├── services/
│   ├── repositories/
│   └── controllers/
│
├── integration/
│   ├── auth/
│   ├── users/
│   └── todos/
│
├── fixtures/
├── factories/
└── setup.js
```

We'll build this gradually rather than creating everything at once.

---

## Lesson 21.1 — Why Backend Testing Matters

We'll start here.

You'll learn:

```text
What is a test?
Why test backend code?
What happens when we don't test?
Manual testing vs automated testing
Regression bugs
Confidence when refactoring
Testing business rules
Testing security boundaries
```

We'll also connect testing to your architecture:

```text
Controller
   ↓
Service
   ↓
Repository
```

For example, if you change your service:

```js
authService.login()
```

you should be able to know whether you accidentally broke:

```text
password verification
token generation
refresh-token handling
error handling
```

without manually opening Postman every time.

---

## Lesson 21.2 — Testing Pyramid

We'll learn the basic model:

```text
             /\
            /  \
           / E2E\
          /------\
         /        \
        /Integration\
       /------------\
      /              \
     /    Unit Tests  \
    /__________________\
```

Generally:

```text
Many unit tests
      +
Some integration tests
      +
Fewer full API/E2E tests
```

We'll discuss **why**.

---

## Lesson 21.3 — Jest Fundamentals

We'll finally get comfortable with:

```bash
npm install -D jest
```

and:

```js
describe()
test()
it()
expect()
```

You'll learn:

```js
describe("something", () => {
    test("should do something", () => {
        expect(...).toBe(...);
    });
});
```

But we won't spend the whole phase learning Jest as a standalone tool.

We'll immediately connect it to your backend.

---

## Lesson 21.4 — Test Structure & Assertions

You'll learn the difference between:

```js
toBe()
toEqual()
toContain()
toThrow()
toHaveBeenCalled()
toHaveBeenCalledWith()
```

and how to structure:

```text
Arrange
   ↓
Act
   ↓
Assert
```

Example:

```text
Arrange
  ↓
create test user

Act
  ↓
call service

Assert
  ↓
user was created
```

This pattern will become your default testing mindset.

---

## Lesson 21.5 — Unit Testing Utilities

We'll start with the easiest layer.

For example:

```text
utils/
├── generateToken.js
├── AppError.js
├── ApiResponse.js
└── ...
```

We'll test things such as:

```text
Does token generation work?
Does AppError contain the correct status?
Does ApiResponse create the expected structure?
```

This gives you your first real unit tests.

---

## Lesson 21.6 — Testing Middleware

Now we'll test:

```text
auth.middleware.js
requestId.middleware.js
role.middleware.js
```

We'll learn how to simulate:

```text
req
res
next
```

For example:

```text
Valid request
   ↓
middleware
   ↓
next()
```

versus:

```text
Invalid request
   ↓
middleware
   ↓
401 / 403
```

This is especially useful because middleware often contains security boundaries.

---

## Lesson 21.7 — Testing Validation

We'll test:

```text
valid body
invalid body
missing field
extra field
wrong type
invalid email
weak password
invalid query
invalid params
```

For example:

```text
POST /users

{
    "email": "wrong"
}
```

should fail **before reaching the service**.

That's an important architectural property we'll verify.

---

## Lesson 21.8 — Testing Services

This will be one of the most important lessons.

Suppose:

```js
authService.login()
```

does:

```text
find user
 ↓
compare password
 ↓
generate tokens
 ↓
save refresh token
 ↓
return result
```

We'll test each business rule.

For example:

```text
Correct password
    → login succeeds

Wrong password
    → login fails

Unknown user
    → login fails

Inactive user
    → login fails

Repository failure
    → error propagates correctly
```

The database won't necessarily be involved in these tests.

---

## Lesson 21.9 — Mocking Dependencies

Now you'll learn **why mocking exists**.

Suppose:

```text
authService
     ↓
userRepository
     ↓
MongoDB
```

When testing the service, we might replace:

```text
MongoDB
```

with:

```text
mock repository
```

So:

```text
authService
     ↓
mockUserRepository
```

This lets us test business logic independently.

You'll learn:

```text
jest.fn()
jest.mock()
mockReturnValue()
mockResolvedValue()
mockRejectedValue()
```

This is where backend testing starts becoming much more powerful.

---

## Lesson 21.10 — Testing Repositories

Now we'll move down a layer.

Repository tests should verify things like:

```text
findById()
findByEmail()
create()
update()
delete()
ownership queries
pagination
filtering
sorting
```

Unlike service tests, repository tests are much closer to the database.

We'll discuss when to:

```text
mock MongoDB
```

and when to use:

```text
real test database
```

---

## Lesson 21.11 — Testing Controllers

Controllers are primarily responsible for:

```text
HTTP input
     ↓
service call
     ↓
HTTP response
```

We'll test:

```text
req.body
req.params
req.query
req.user
status code
response body
service errors
```

We don't want controller tests to duplicate all the business-logic tests from the service layer.

That's an important lesson.

---

## Lesson 21.12 — Integration Testing

Now we connect multiple layers.

Instead of:

```text
service
   ↓
mock repository
```

we can test:

```text
service
   ↓
repository
   ↓
database
```

This catches bugs that unit tests can't.

For example:

```text
Service expects:
findUserByEmail()

Repository actually provides:
findByEmail()
```

Unit tests with excessive mocking might miss this.

Integration tests can catch it.

---

## Lesson 21.13 — Supertest

Now we test the actual HTTP layer.

We'll use:

```bash
npm install -D supertest
```

Then:

```text
HTTP request
   ↓
Express app
   ↓
route
   ↓
middleware
   ↓
controller
   ↓
service
```

For example:

```text
POST /api/v1/auth/signup
```

We'll test:

```text
status code
response body
headers
cookies
authentication
validation
errors
```

This is where your backend starts being tested like a real API.

---

## Lesson 21.14 — Testing Authentication

We'll create tests for:

```text
Signup
Login
Refresh token
Logout
Password reset
Email verification
```

Examples:

```text
Valid login
→ 200

Wrong password
→ 401

Unknown user
→ 401

Expired token
→ 401

Invalid refresh token
→ 401

Logout
→ refresh token invalidated
```

We'll also test security-sensitive behavior rather than only successful cases.

---

## Lesson 21.15 — Testing Authorization

This is extremely important.

We'll test:

```text
Unauthenticated user
      ↓
401

Authenticated normal user
      ↓
403 for admin route

Admin
      ↓
allowed
```

And ownership:

```text
User A
  ↓
Todo A → allowed

User A
  ↓
Todo B → denied
```

This directly tests the authorization architecture you've already learned.

---

## Lesson 21.16 — Testing CRUD APIs

Now we'll take your Phase 17 CRUD architecture and test it completely.

For example:

```text
POST   /todos
GET    /todos
GET    /todos/:id
PATCH  /todos/:id
DELETE /todos/:id
```

We'll test:

```text
success
validation
authentication
authorization
not found
duplicate data
ownership
pagination
filtering
sorting
errors
```

At this point, your CRUD API becomes a properly tested feature rather than just working in Postman.

---

## Lesson 21.17 — Test Database & Isolation

This is a major real-world concept.

We don't want:

```text
Test 1
  ↓
creates user

Test 2
  ↓
unexpectedly sees user from Test 1
```

We'll learn:

```text
test database
database cleanup
beforeAll
beforeEach
afterEach
afterAll
test isolation
transactions where useful
```

The goal:

> Every test should behave predictably regardless of test order.

---

## Lesson 21.18 — Fixtures, Factories & Coverage

As your test suite grows, manually creating objects becomes painful.

We'll introduce:

```text
fixtures
factories
test helpers
```

For example:

```js
createTestUser()
createTestTodo()
generateAuthToken()
```

Then we'll learn coverage:

```bash
npm test -- --coverage
```

We'll discuss why:

```text
90% coverage
```

does **not automatically mean**

```text
90% quality
```

Coverage is a measurement, not proof of correctness.

---

# Lesson 21.19 — Build the Complete Backend Test Architecture

This will be the final lesson.

We'll combine everything:

```text
                    HTTP TEST
                        │
                        ▼
                     ROUTE
                        │
                        ▼
                   MIDDLEWARE
                        │
              ┌─────────┴─────────┐
              │                   │
          Validation            Auth
              │                   │
              └─────────┬─────────┘
                        ▼
                   CONTROLLER
                        │
                        ▼
                     SERVICE
                        │
                        ▼
                   REPOSITORY
                        │
                        ▼
                   TEST DB
```

And alongside that:

```text
Unit tests
    ↓
Service tests
    ↓
Repository tests
    ↓
Integration tests
    ↓
API tests
```

We'll finish by creating the testing structure for your actual MERN backend starter.

---

# The testing mindset I want you to develop

Don't think:

> "I need to write tests because projects require tests."

Think:

> **"What behavior must never break?"**

For example:

```text
Password must never be stored in plaintext.
```

Test it.

```text
User A must never access User B's resource.
```

Test it.

```text
Invalid input must never reach business logic.
```

Test it.

```text
Expired access token must not authenticate a request.
```

Test it.

```text
Deleting a resource should only affect the owner's resource.
```

Test it.

These are **engineering guarantees**, not just test cases.

---

# Phase 21 → Phase 22

Once Phase 21 is complete, we'll move into:

```text
Phase 22
Security Testing
```

There we'll deliberately attack the backend:

```text
IDOR
Broken authorization
JWT attacks
Refresh-token abuse
Injection
Mass assignment
Rate-limit bypass
CORS mistakes
CSRF
Sensitive data exposure
```

So the sequence becomes:

```text
Build it
   ↓
Test that it works
   ↓
Attack it
   ↓
Fix it
   ↓
Deploy it
```

That's a much stronger backend engineering workflow.

**Start with `lesson 21.1` whenever you're ready.**