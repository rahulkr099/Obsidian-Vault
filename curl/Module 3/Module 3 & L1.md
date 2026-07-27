# 🚀 curl Mastery Course

# Module 3 — Advanced HTTP & API Testing

**Difficulty:** ⭐⭐⭐⭐☆ → ⭐⭐⭐⭐⭐  
**Estimated Time:** 15–20 Hours

> **Goal:** Learn how professional backend engineers, DevOps engineers, SREs, QA engineers, and API developers use `curl` for debugging, automation, security testing, performance analysis, and production troubleshooting.

This module moves beyond "sending requests" and focuses on understanding **how HTTP actually works**.

---

# 📚 Module 3 Roadmap

|Lesson|Topic|Difficulty|
|---|---|---|
|1|Cookies & Sessions|⭐⭐⭐⭐☆|
|2|Custom Headers Deep Dive|⭐⭐⭐⭐☆|
|3|HTTP Authentication (Basic, Bearer, API Keys)|⭐⭐⭐⭐☆|
|4|HTTPS, SSL & Certificates|⭐⭐⭐⭐⭐|
|5|Redirects & URL Handling|⭐⭐⭐⭐☆|
|6|Timeouts, Retries & Connection Management|⭐⭐⭐⭐⭐|
|7|Compression & Content Encoding|⭐⭐⭐⭐☆|
|8|HTTP Caching (ETag, Cache-Control)|⭐⭐⭐⭐⭐|
|9|Rate Limiting & API Reliability|⭐⭐⭐⭐⭐|
|10|Production Debugging Toolkit|⭐⭐⭐⭐⭐|

---

# What You'll Build

By the end of Module 3, you'll be able to debug problems like:

✅ Login sessions not working

✅ Cookies disappearing

✅ HTTPS certificate failures

✅ Infinite redirects

✅ SSL handshake issues

✅ API timeouts

✅ Slow responses

✅ Cache problems

✅ Rate limit errors (429)

✅ Authentication failures

These are real problems backend developers solve regularly.

---

# Skills You'll Gain

You'll learn how to:

- Debug authentication
    
- Work with cookies
    
- Handle browser sessions
    
- Understand HTTPS
    
- Analyze response headers
    
- Measure response time
    
- Retry failed requests
    
- Simulate browser behavior
    
- Test production APIs safely
    
- Investigate networking issues
    

---
# 🥇 Module 3 — Lesson 1

# Cookies & Sessions

**Difficulty:** ⭐⭐⭐⭐☆

**Estimated Time:** 90 minutes

---

# 🎯 Learning Objectives

By the end of this lesson you will understand:

- What cookies are
    
- Why sessions need cookies
    
- How browsers store cookies
    
- How `curl` stores cookies
    
- Cookie jars (`-c`)
    
- Sending cookies (`-b`)
    
- Login sessions
    
- Session authentication
    

---

# 1. What Is a Cookie?

A cookie is a **small piece of data** that a server asks the client to store and send back on future requests.

Example:

```text
Name: sessionId

Value: abc123xyz
```

---

# 2. Why Cookies Exist

Imagine logging into a website.

```
Login

↓

Server verifies password

↓

Server creates session

↓

Server gives browser a cookie

↓

Browser stores cookie

↓

Future requests include cookie

↓

Server recognizes you
```

Without cookies, the server would forget who you are after every request.

---

# 3. Cookie Example

Server response:

```http
HTTP/1.1 200 OK

Set-Cookie: sessionId=abc123
```

Browser stores:

```
sessionId=abc123
```

Next request:

```http
GET /profile

Cookie: sessionId=abc123
```

---

# 4. Inspect Cookies with `curl`

Request:

```bash
curl -i https://httpbin.org/cookies/set/name/Rahul
```

Response:

```http
Set-Cookie: name=Rahul
```

Notice:

```
Set-Cookie
```

comes **from the server**.

---

# 5. Save Cookies (`-c`)

Browsers save cookies automatically.

`curl` doesn't.

Instead:

```bash
curl \
-c cookies.txt \
https://httpbin.org/cookies/set/name/Rahul
```

Now inspect:

```bash
cat cookies.txt
```

Example:

```
httpbin.org    FALSE   /   FALSE   0   name   Rahul
```

---

# 6. Send Cookies (`-b`)

Now reuse them:

```bash
curl \
-b cookies.txt \
https://httpbin.org/cookies
```

Response:

```json
{
  "cookies": {
    "name": "Rahul"
  }
}
```

---

# 7. Save and Send Together

Very common:

```bash
curl \
-c cookies.txt \
-b cookies.txt \
https://httpbin.org/cookies/set/name/Rahul
```

Meaning:

- Save new cookies
    
- Send existing cookies
    

This is how you maintain a session across multiple requests.

---

# 8. Manual Cookies

You can also send cookies directly.

```bash
curl \
-b "theme=dark"
```

Or:

```bash
curl \
-b "sessionId=abc123"
```

Or multiple:

```bash
curl \
-b "theme=dark; language=en"
```

---

# 9. Login Example

POST:

```bash
curl \
-c cookies.txt \
-d "email=rahul@example.com&password=secret123" \
http://localhost:3000/login
```

Server returns:

```http
Set-Cookie: sessionId=abc123
```

Saved automatically.

---

# 10. Access Protected Route

```bash
curl \
-b cookies.txt \
http://localhost:3000/profile
```

Now the server knows who you are.

---

# 11. Cookies vs JWT

|Cookies|JWT|
|---|---|
|Stored by browser|Stored by client|
|Automatic|Must send manually|
|Good for sessions|Good for APIs|
|Traditional web apps|REST APIs|
|Sent as `Cookie` header|Sent as `Authorization` header|

Modern REST APIs often use JWTs, but many web applications still rely on cookie-based sessions.

---

# 12. Cookie Attributes

Example:

```http
Set-Cookie:
sessionId=abc123;
HttpOnly;
Secure;
SameSite=Lax
```

Common attributes:

|Attribute|Purpose|
|---|---|
|`HttpOnly`|JavaScript can't read the cookie|
|`Secure`|Send only over HTTPS|
|`SameSite`|Helps protect against CSRF attacks|
|`Expires`|Expiration date|
|`Max-Age`|Lifetime in seconds|
|`Path`|Restricts URL path|
|`Domain`|Restricts domain|

---

# 13. Debugging Cookie Problems

If login doesn't persist:

✅ Did the server send `Set-Cookie`?

```bash
curl -i ...
```

---

✅ Did you save cookies?

```bash
-c cookies.txt
```

---

✅ Did you send them back?

```bash
-b cookies.txt
```

---

✅ Is the cookie expired?

```bash
cat cookies.txt
```

---

# 14. Common Mistakes

❌ Forgetting `-c`

Nothing gets saved.

---

❌ Forgetting `-b`

Cookies never get sent.

---

❌ Deleting `cookies.txt`

Session is lost.

---

❌ Using JWT and cookies interchangeably

They solve similar problems but are transmitted differently.

---

# 15. Real Backend Workflow

```text
Login
   │
   ▼
Receive Set-Cookie
   │
   ▼
Save Cookie
   │
   ▼
Send Cookie
   │
   ▼
Access Dashboard
   │
   ▼
Logout
```

---

# 💻 Hands-on Practice

### Exercise 1

Save a cookie:

```bash
curl \
-c cookies.txt \
https://httpbin.org/cookies/set/user/Rahul
```

---

### Exercise 2

View the cookie:

```bash
cat cookies.txt
```

---

### Exercise 3

Send it back:

```bash
curl \
-b cookies.txt \
https://httpbin.org/cookies | jq
```

---

### Exercise 4

Send a manual cookie:

```bash
curl \
-b "theme=dark" \
https://httpbin.org/cookies | jq
```

Observe how the server echoes the cookie.

---

# 🏆 Mini Challenge

Using `httpbin`:

1. Create two cookies:
    
    - `user=Rahul`
        
    - `theme=dark`
        
2. Save them in `cookies.txt`.
    
3. Send them back using `-b`.
    
4. Verify the response contains both cookies.
    
5. Delete `cookies.txt` and observe how the session information is lost.
    

---

# 📚 Lesson Summary

Today you learned:

- What cookies are
    
- The difference between `Set-Cookie` and `Cookie`
    
- How to save cookies with `-c`
    
- How to send cookies with `-b`
    
- How cookie-based sessions work
    
- How cookies differ from JWT authentication
    
- Common cookie debugging techniques
    

---

# 💡 Pro Tips

### 1. Use one cookie jar per environment

```text
cookies-dev.txt
cookies-staging.txt
cookies-prod.txt
```

This prevents mixing sessions between environments.

---

### 2. Inspect headers when debugging

```bash
curl -i \
-c cookies.txt \
http://localhost:3000/login
```

Seeing the `Set-Cookie` header often explains session issues immediately.

---

### 3. Never commit cookie files

Add them to `.gitignore`:

```text
cookies*.txt
```

They may contain active session identifiers.

---

# 🎯 Homework

Build a simple Express app using `express-session` with:

- `POST /login`
    
- `GET /profile`
    
- `POST /logout`
    

Test the entire login flow using only `curl`:

1. Log in and save cookies.
    
2. Access the protected profile route.
    
3. Log out.
    
4. Confirm that accessing the profile route again fails because the session is gone.
    

---

## ⏭️ Next Lesson

**Module 3 – Lesson 2: Custom Headers Deep Dive**

You'll learn:

- How HTTP headers really work
    
- Request vs response headers
    
- `User-Agent`
    
- `Accept`
    
- `Accept-Language`
    
- `Accept-Encoding`
    
- `Origin`
    
- `Referer`
    
- Custom `X-*` headers
    
- Advanced debugging with headers
